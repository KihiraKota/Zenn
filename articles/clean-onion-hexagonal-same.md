---
title: "クリーンアーキテクチャとオニオンとヘキサゴナルの違い？残念だがそんなものは無い！"
emoji: "👏" # todo 絵文字の選定
type: "tech" # tech: 技術記事 / idea: アイデア
topics: [ヘキサゴナルアーキテクチャ, オニオンアーキテクチャ, クリーンアーキテクチャ, アプリケーションアーキテクチャ, ソフトウェアアーキテクチャ]
published: false
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
このような置き換えをする場合に、アプリケーションに大きな変更をしなくても対応ができる構造として考えられたのが、これら3つのアーキテクチャです。

- **外部の要素**
    - **アプリケーションを利用するもの** 例:ユーザー、外部システム
    - **アプリケーションが利用するもの** 例: データベース、外部API
    - **外部ライブラリ** 例: フレームワーク、ドライバー

### そのために何をするのか？

todo 続きはここから。以下、メモ。

そしてそのために何をするのかというと、

1. システムの最も内側に、外部の要素には依存しないビジネスルール用のレイヤーを作る
2. ビジネスルール用のレイヤーの外側に、外部の要素とビジネスルール用のレイヤーを仲介するインターフェイス用のレイヤーを作る

これら２つのレイヤーを作っておくことで、外部の要素が何に置き換わったとしても、ビジネスルール用のレイヤーには何も変更を加えることなく、実行やテストができるようにします。

## 要点との対応

それではここからは、上記の要点が3つのアーキテクチャにそれぞれどう対応しているのかを見ていきます。

### ヘキサゴナルアーキテクチャ

> ![ヘキサゴナルアーキテクチャ](/images/ref-HexagonalArchitecture.gif)
> 
> 出典: [The Hexagonal (Ports & Adapters) Architecture | Alistair Cockburn](https://alistair.cockburn.us/hexagonal-architecture/)

2005年に[Alistair Cockburn](https://alistaircockburn.com/Bio)氏が公開したアーキテクチャです。

https://alistair.cockburn.us/hexagonal-architecture/

(driving) Adapter
(driven) Adapter

### オニオンアーキテクチャ

> ![オニオンアーキテクチャ](/images/ref-OnionArchitecture.png)
> 
> 出典: [The Onion Architecture : part 1 | Programming with Palermo](https://jeffreypalermo.com/2008/07/the-onion-architecture-part-1/)

2008年に[Jeffrey Palermo](https://jeffreypalermo.com/about/)氏が公開したアーキテクチャです。

https://jeffreypalermo.com/2008/07/the-onion-architecture-part-1/

### クリーンアーキテクチャ

> ![クリーンアーキテクチャ](/images/ref-CleanArchitecture.jpg)
> 
> 出典: [The Clean Architecture | The Clean Code Blog](https://blog.cleancoder.com/uncle-bob/2012/08/13/the-clean-architecture.html)

2012年に[Robert C. Martin](https://en.wikipedia.org/wiki/Robert_C._Martin)氏が公開したアーキテクチャです。

https://blog.cleancoder.com/uncle-bob/2012/08/13/the-clean-architecture.html

## ドメイン駆動設計 todo 見出しを考える

![](/images/clean-onion-hexagonal-same2.png)

todo ぶっちゃけDDDだよね。

## 参考書籍・参考資料

todo 人のリンク貼る？

* [エンタープライズアプリケーションアーキテクチャパターン](https://www.shoeisha.co.jp/book/detail/9784798105536) (Martin Fowler, 2002)
* [エリック・エヴァンスのドメイン駆動設計](https://www.shoeisha.co.jp/book/detail/9784798121963) (Eric Evans, 2003)
* [The Hexagonal (Ports & Adapters) Architecture](https://alistair.cockburn.us/hexagonal-architecture/) (Alistair Cockburn, 2005)
* [The Onion Architecture](https://jeffreypalermo.com/2008/07/the-onion-architecture-part-1/) (Jeffrey Palermo, 2008)
* [The Clean Architecture](https://blog.cleancoder.com/uncle-bob/2012/08/13/the-clean-architecture.html) (Robert C. Martin, 2012)
