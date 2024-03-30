---
title: "Laravelでのリクエストパラメーターのリファクタリング"
emoji: "🦝"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: [laravel]
published: false
---
Laravelでそれなりに規模の大きいAPIの開発をしていると、リクエストパラメーターを整理しなければいけない場面が出てきます。しかしLaravelの基礎的な機能だけを使ってリクエストパラメーターを扱っていると、なかなか整理がしづらいことがあるため、そうならないようにするためのリファクタリングの方法です。

## 要点

まず大前提として重要なのが、 __エディターやIDEのリファクタリング機能が使える状態にする__ 、ということです。

それなりに規模の大きい開発ではたくさんの `Model` が必要になり、複数の `Model` が同じ名前のプロパティを持っている、ということはよくあります。例えば、「名前」を表す「name」というプロパティは、多くの `Model` が持っているのではないでしょうか。そのような場合に、リネームが必要な `Model` のプロパティだけを正確にリネームするのは文字列の検索だけでは難しく、エディターやIDEのリファクタリング機能が使える状態になっていた方が圧倒的に作業が簡単です。

そのために必要なリファクタリングをしていくのですが、要点をまとめると以下の２点です。

- __リクエストパラメーターは `Request` クラスで形を整える__
- __必要に応じてパラメーター用のクラスを作る__

## 第０段階：Laravelの基礎的な機能だけを使う

以下、例として「記事(=Article)」という `Model` に、「題名(=title)」と「本文(=body)」というプロパティがあるものとして話を進めます。

Laravelの基礎的な機能だけを使って「記事」を作成するAPIを作成する場合、以下のようなコードになるかと思いす。

```php:app/Http/Controllers/ArticleController.php
/**
 * 記事コントローラー
 */
class ArticleController extends Controller
{
    /**
     * 記事を作成する
     *
     * @param Request $request
     * @return Article
     */
    public function store(Request $request): Article
    {
        return Article::create($request->all());
    }
}
```

リクエストパラメーターとして受け取った値をそのまま `Article` の `Model` に流し込んでDBに保存しているわけですが、主に以下の問題があります。

- `Article` のどのプロパティを操作しているのかがコードを見ても分からない
- リクエストパラメーターのキーの名前と、DBのカラムの名前が必ず一致している必要がある

## 第１段階：操作するプロパティを明示する

まず、 `Article` のどのプロパティを操作しているのかを明示するようにします。前述したコードよりも記述量は増えてしまいますが、どのプロパティを操作しているのかが分からない状態では後から修正を加えることができません。

```php:app/Http/Controllers/ArticleController.php
    /**
     * 記事を作成する
     *
     * @param Request $request
     * @return Article
     */
    public function store(Request $request): Article
    {
        $article = new Article();
        $article->title = $request->input('title');
        $article->body = $request->input('body');
        $article->save();

        return $article;
    }
```

## 第２段階：リクエストパラメーターの値を文字列で指定して取得するのをやめる

次に、リクエストパラメーターの値の取得方法を改良します。クライアントサイドとサーバーサイドを同じ人間が開発している場合はそれほど問題にはならないかもしれませんが、別の人間が開発する場合はリクエストパラメーターのキーの名前とDBのカラムの名前を必ず一致させられるとは限りません。Laravelの `Request` クラスを拡張し、リクエストパラメーターのキーの名前に依存しないコードにします。

```php:app/Http/Requests/Article/StoreRequest.php
/**
 * 記事を作成するリクエスト
 */
class StoreRequest extends Request
{
    /**
     * 題名の値を返す
     *
     * @return string
     */
    public function title(): string
    {
        return $this->input('title');
    }

    /**
     * 本文の値を返す
     *
     * @return string
     */
    public function body(): string
    {
        return $this->input('body');
    }
}
```

```php:app/Http/Controllers/ArticleController.php
    /**
     * 記事を作成する
     *
     * @param StoreRequest $request
     * @return Article
     */
    public function store(StoreRequest $request): Article
    {
        $article = new Article();
        $article->title = $request->title();
        $article->body = $request->body();
        $article->save();

        return $article;
    }
```

## 第３段階：パラメーターをまとめるためのクラスを作る

前述のコードを見て、「題名」と「本文」の値を返すだけのメソッドをいちいち作るのが面倒だ、と思う方がいらっしゃるかと思います。まったくもってその通りで、パラメーターが複数あるのであれば、それをまとめるためのクラスを作成した方が扱いやすい場合があります。必ずしもパラメーターをまとめた方が良いとは限りませんが、１つの `Model` のプロパティであれば、ほとんどの場合まとめてしまった方が良いはずです。

```php:app/Models/ArticleModelParam.php
/**
 * 記事モデルパラメーター
 */
class ArticleModelParam
{
    /**
     * コンストラクタ
     *
     * @param string $title
     * @param string $body
     */
    public function __construct(
        public string $title,
        public string $body,
    )
    {
    }
}
```

```php:app/Http/Requests/Article/StoreRequest.php
/**
 * 記事を作成するリクエスト
 */
class StoreRequest extends Request
{
    /**
     * 記事モデルパラメーターを返す
     *
     * @return ArticleModelParam
     */
    public function articleModelParam(): ArticleModelParam
    {
        return new ArticleModelParam(
            title: $this->input('title'),
            body: $this->input('body'),
        );
    }
}
```

```php:app/Http/Controllers/ArticleController.php
    /**
     * 記事を作成する
     *
     * @param StoreRequest $request
     * @return Article
     */
    public function store(StoreRequest $request): Article
    {
        $param = $request->articleModelParam();

        $article = new Article();
        $article->title = $param->title;
        $article->body = $param->body;
        $article->save();

        return $article;
    }
```

## まとめ

上記のリファクタリングによって、リクエストパラメーターにどんな変更が必要になっても、その変更はすべて `Request` クラスで吸収することができ、APIの処理の本体には一切変更をする必要がなくなります。また、エディターやIDEのリファクタリング機能を使うことで、プロパティ名の変更なども簡単にできるようになります。
