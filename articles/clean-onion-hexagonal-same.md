---
title: "クリーンアーキテクチャとオニオンとヘキサゴナルの違い？残念だがそんなものは無い！"
emoji: "😈"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: [ヘキサゴナルアーキテクチャ, オニオンアーキテクチャ, クリーンアーキテクチャ, アプリケーションアーキテクチャ, ソフトウェアアーキテクチャ]
published: true
---
## はじめに

**Q: クリーンとオニオンとヘキサゴナル、この3つのアーキテクチャは何が違うの？**
**A: 違いはありません。すべて同じです。**

最初に結論を言ってしまいますが、クリーンアーキテクチャ、オニオンアーキテクチャ、ヘキサゴナルアーキテクチャ、これらはすべて同じアプリケーションアーキテクチャです。

もちろんそれぞれのアーキテクチャで登場する用語などは異なりますので、違いがまったくないわけではありませんが、そのような細かな違いは本質的なものではありません。
「United States of America」のことを「USA」といっても「アメリカ」といっても「米国」といっても大きな違いはないのと同じです。

実際にクリーンアーキテクチャを採用して書かれたコードを見て、「これはオニオンアーキテクチャだ」と言うことは可能ですし、逆にオニオンアーキテクチャを採用して書かれたコードを見て、「これはクリーンアーキテクチャではない」と言うことも不可能です。
どのアーキテクチャを採用してもコードに本質的な違いがないのですから、 **すべて同じといって何の問題もありません。**

## 3つのアーキテクチャの要点

![3つのアーキテクチャの要点](/images/clean-onion-hexagonal-same1.png)

上の図は、3つのアーキテクチャの要点と、それぞれのアーキテクチャに登場する用語がどう対応するのかをまとめたものです。

直角の長方形はアプリケーション内のレイヤーを表し、角丸の長方形はアプリケーション外の要素を表しています。
また、レイヤー内のレイヤーの上下は、すべて「上のレイヤーが下のレイヤーに依存する」という関係を表しています。

### どんな問題を解決したいのか？

ヘキサゴナル、オニオン、クリーン、これら3つのアーキテクチャはすべて、 **「外部の要素を別のものに置き換える場合に、アプリケーションに大きな変更が発生してしまう」** という問題を解決するためにあります。

ここでいう外部の要素というのは、アプリケーションを利用するユーザーや、アプリケーションがデータを保存するためのデータベース、アプリケーションが土台にしているフレームワークなどのことです。

ユーザーがこれまでGUIで直接操作していたものを自動化するためにCUIでも操作できるようにする。データベースをMySQLからPostgreSQLに切り替える。フレームワークをCakePHPからLaravelに移行する。
このような置き換えをする場合に、アプリケーションに大きな変更をしなくても対応ができるように考えられたのが、これら3つのアーキテクチャです。

- **外部の要素**
    - **アプリケーションを利用するもの** 例:ユーザー、外部システム
    - **アプリケーションが利用するもの** 例: データベース、外部API
    - **外部ライブラリ** 例: フレームワーク、ドライバー

### そのために何をするのか？

3つのアーキテクチャは、以下のようにすることで、上記の問題を解決しています。

1. アプリケーションの中心に、外部の要素には一切依存しないレイヤーを作る
2. 1.のレイヤーと外部の要素を仲介するレイヤーを作る

このようなレイヤーの構造にすることで、外部の要素を別のものに置き換える場合でも、1.のレイヤーには大きな変更をしなくても良いようにしているのです。

上の図の要点では、1.のレイヤーのことを **「ドメイン層」** 、2.のレイヤーを役割ごとに分け、「アプリケーションを利用するもの」との仲介をするレイヤーを **「UI層」** 、「アプリケーションが利用するもの」との仲介をするレイヤーを **「インフラ層」** としています。

- **ドメイン層**
    - 役割: 外部の要素が別のものに置き換わっても変わらない、アプリケーションの本質的な処理を実行する。
    - 依存関係: 外部の要素には一切依存しない
- **UI層**
    - 役割: 「ドメイン層」と「アプリケーションを利用するもの」を仲介する。
    - 依存関係: 「ドメイン層」と「外部ライブラリ」に依存する。
- **インフラ層**
    - 役割: 「ドメイン層」と「アプリケーションが利用するもの」を仲介する。
    - 依存関係: 「ドメイン層」と「外部ライブラリ」、「アプリケーションが利用するもの」に依存する。

## 要点との対応

それではここからは、上記の要点とそれぞれのアーキテクチャがどう対応しているのかを見ていきます。

### ヘキサゴナルアーキテクチャ

> ![ヘキサゴナルアーキテクチャ](/images/ref-HexagonalArchitecture.gif)
> 
> 出典: [The Hexagonal (Ports & Adapters) Architecture | Alistair Cockburn](https://alistair.cockburn.us/hexagonal-architecture/)

#### ドメイン層

中央にある「Application」がドメイン層にあたります。

#### UI層

「Application」の左側にある「Adapter」がUI層にあたります。

図には反映されていませんが、[原文](https://alistair.cockburn.us/hexagonal-architecture/)の中では、

> *driving* adapters

とも表現されていて、「○○がApplicationを動かすためのアダプター」という意味になっています。

#### インフラ層

「Application」の右側にある「Adapter」がインフラ層にあたります。

図には反映されていませんが、こちらも[原文](https://alistair.cockburn.us/hexagonal-architecture/)の中では、

> *driven* adapters

とも表現されていて、「Applicationが○○を動かすためのアダプター」という意味になっています。

### オニオンアーキテクチャ

> ![オニオンアーキテクチャ](/images/ref-OnionArchitecture.png)
> 
> 出典: [The Onion Architecture : part 1 | Programming with Palermo](https://jeffreypalermo.com/2008/07/the-onion-architecture-part-1/)

#### ドメイン層

中央にある「Application Core」がドメイン層にあたります。

「Application Core」の中が更に細かくレイヤー分けされていて、以下のような依存関係になっていますが、「Application Core」がドメイン層にあたる、ということは変わりません。

- **Application Services** : Domain Services と Domain Model に依存する
- **Domain Services** : Domain Modelに依存する
- **Domain Model** : 何にも依存しない

#### UI層

円の一番外側の上にある「User Interface」がUI層にあたります。そのままですね。

#### インフラ層

円の一番外側の右下にある「Infrastructure」がインフラ層にあたります。こちらもそのままです。

「Infrastructure」から出ている矢印の先にある「Web Interface」「File」「DB」といったものが、まさに「アプリケーションが利用するもの」です。

### クリーンアーキテクチャ

> ![クリーンアーキテクチャ](/images/ref-CleanArchitecture.jpg)
> 
> 出典: [The Clean Architecture | The Clean Code Blog](https://blog.cleancoder.com/uncle-bob/2012/08/13/the-clean-architecture.html)

:::message
クリーンアーキテクチャの図を見る上での注意点
:::

ここで一つ注意が必要なのが、青色の「Frameworks & Drivers」です。

ヘキサゴナルの図の六角形や、オニオンの図の円と同様に、全体を囲う大きな枠の中に入っている要素なので、これもアプリケーションの一部のように見えますが、**「Frameworks & Drivers」はアプリケーションの一部ではなく、「外部の要素」にあたります。**

[原文](https://blog.cleancoder.com/uncle-bob/2012/08/13/the-clean-architecture.html)の「Frameworks and Drivers」のセクションでも、

> The outermost layer is generally composed of frameworks and tools such as the Database, the Web Framework, etc.
> 
> 訳: 一番外側の層は、通常、データベースやWebフレームワークなどのフレームワークやツールによって構成される。

> This layer is where all the details go. The Web is a detail. The database is a detail. We keep these things on the outside where they can do little harm.
> 
> 訳: この層は、すべての「詳細」が配置される場所である。Webは詳細である。データベースは詳細である。私たちは、これらの要素が内側の円に害を及ぼさないよう、ここに隔離しておく。

とあるように、「Frameworks & Drivers」は「外部の要素」です。

だとしたら「Frameworks & Drivers」から円の内側に向かっている矢印はどうなるんだ？ということになるのですが、この矢印は「○○は××があることを知っている」という「依存」の関係の矢印ではなく、「○○は××とつながっている」という「接続」の関係の矢印だと捉えるのが自然です。
「Frameworks & Drivers」を「外部の要素」としている以上、**「Frameworks & Drivers」がアプリケーションのことを知っている、ということはありえません。**

以上のことを踏まえて、要点とクリーンアーキテクチャがどう対応しているのかを見てみると、以下のようになります。

#### ドメイン層

赤色の「Application Business Rules」と黄色の「Enterprise Business Rules」を合わせたものがドメイン層にあたります。

また、依存関係は以下のようになっています。

- **Application Business Rules** : Enterprise Business Rulesに依存する
- **Enterprise Business Rules** : 何にも依存しない

#### UI層

緑色の「Interface Adapters」の一部がUI層にあたります。

ドメイン層と○○との仲介をする、という役割別ではレイヤーが分かれていませんが、図の中にある要素でいうと、「Controllers」と「Presenters」がUI層にあたります。

#### インフラ層

緑色の「Interface Adapters」の一部がインフラ層にあたります。

ドメイン層と○○との仲介をする、という役割別ではレイヤーが分かれていませんが、図の中にある要素でいうと、「Gateways」がインフラ層にあたります。

## まとめ

さて、ここまでの話で、ヘキサゴナル、オニオン、クリーン、という3つのアーキテクチャは、すべて同じものだということにご納得いただけたでしょうか？

唯一これらに違いがあるとすれば、ドメイン層の中のレイヤーの分け方くらいのものですが、ドメイン層の中を分けていないヘキサゴナルでも、オニオンのApplication Servicesや、クリーンのApplication Business RulesにあるUse Casesに相当するクラスは作ります。結局のところ、図に描いてあるのかないのかの違いで、どのアーキテクチャを採用しても本質的には同じようなコードを書くのです。

それでは最後に、これらのアーキテクチャの些末な違いに囚われて不毛な時間を過ごすことになる人が一人でも減ることを祈りつつ、一発かましてまとめとさせて頂きます。

**ヘキサゴナル、オニオン、クリーンに違いなどありません！**
**どれでもいいからサッサと開発を進めましょう！**

## おまけ①：3つのアーキテクチャの正体

記事の本文では、3つのアーキテクチャの要点をまとめ、これら3つは同じ、としていましたが、これは別に私が独自にまとめた要点でもなんでもなく、「ドメイン駆動設計」が元ネタです。

![3つのアーキテクチャの正体](/images/clean-onion-hexagonal-same2.png)

上の図は、冒頭の要点の図に、ドメイン駆動設計のレイヤードアーキテクチャを追加したものです。

厳密にはドメイン駆動設計が本の中で直接示したアーキテクチャとは異なりますが、それ以前の「ドメイン層がインフラ層に依存する構造」ではなく、「インフラ層がドメイン層に依存する構造」にすれば、外部の要素を置き換えてもドメイン層には大きな変更が発生しないようにできる、というドメイン駆動設計のアイディアをまとめると、上の図のようなアーキテクチャになります。

ヘキサゴナル、オニオン、クリーンは、このドメイン駆動設計と同じアイディアをそれぞれの人がそれぞれの時期に上手くアーキテクチャに落とし込もうとした結果生まれたもの、ということができますね。

## おまけ②：クリーンアーキテクチャの依存関係

記事の本文では、話を単純化するため、「Frameworks & Drivers」から円の内側に向かう矢印は「接続」の関係の矢印、としましたが、厳密にはこの矢印は「依存」の関係の矢印です。

これは「Frameworks and Drivers」に含まれているものが「外部の要素」だけではなく、「アプリケーションのコード」も含まれているためで、[原文](https://blog.cleancoder.com/uncle-bob/2012/08/13/the-clean-architecture.html)の「Frameworks and Drivers」のセクションにある `glue code` というものが、この「アプリケーションのコード」にあたります。

> Generally you don’t write much code in this layer other than glue code that communicates to the next circle inwards.
> 
> 訳: 一般的に、この層では、内側の次の層と通信するための接着剤のようなコード以外は、あまり多くのコードを記述しません。

![クリーンアーキテクチャの依存関係](/images/clean-onion-hexagonal-same3.png)

上の図は、[原文](https://blog.cleancoder.com/uncle-bob/2012/08/13/the-clean-architecture.html)の「Frameworks and Drivers」のセクションにある `glue code` と `details` を分離したものです。

クリーンアーキテクチャでは、プログラミング言語の標準機能などを使って `details` にはまったく依存しない形で「Interface Adapters」を作成し、その上で `glue code` が「Interface Adapters」と `details` をつなぐようにしています。そのため `glue code` も含めた「Frameworks & Drivers」で考えると、円の内側に向かう矢印は「依存」の関係の矢印、ということになるのです。

若干複雑にはなりましたが、しかしこの `glue code` を含めても、ドメイン層の中のレイヤーと同じく、あくまでもこれはUI層やインフラ層の中をどこまで細かく分けるのか、という違いで、本質的には他のアーキテクチャと変わりません。

---

さて、ここまでで何度も「ヘキサゴナル、オニオン、クリーンは同じ」と言ってきましたし、本文のまとめでも「どれでもいい」と言っておいてなんなのですが、私はクリーンアーキテクチャは人には薦めていません。

理由は簡単で、このおまけで書いた通り、「アプリケーション」と「外部の要素」の境界がどこにあるのかがハッキリしていないからです。
これが余計な誤解や混乱を生む原因になっていると思っています。

「クリーンアーキテクチャでリポジトリの実装はどの層に置くの？」と聞かれて、「Frameworks & Drivers」と答えてしまう人、多分たくさんいますよね？

## 参考書籍・参考資料

* [エンタープライズアプリケーションアーキテクチャパターン](https://www.shoeisha.co.jp/book/detail/9784798105536) (Martin Fowler, 2002)
* [エリック・エヴァンスのドメイン駆動設計](https://www.shoeisha.co.jp/book/detail/9784798121963) (Eric Evans, 2003)
* [The Hexagonal (Ports & Adapters) Architecture](https://alistair.cockburn.us/hexagonal-architecture/) (Alistair Cockburn, 2005)
* [The Onion Architecture](https://jeffreypalermo.com/2008/07/the-onion-architecture-part-1/) (Jeffrey Palermo, 2008)
* [The Clean Architecture](https://blog.cleancoder.com/uncle-bob/2012/08/13/the-clean-architecture.html) (Robert C. Martin, 2012)
