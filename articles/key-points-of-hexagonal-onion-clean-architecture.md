---
title: "Hexagonal, Onion, Clean Architectureの超ザックリとした要点"
emoji: "🦝"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: [ヘキサゴナルアーキテクチャ, オニオンアーキテクチャ, クリーンアーキテクチャ]
published: true
---
Hexagonal Architecture、Onion Architecture、Clean Architecture、これらのアーキテクチャーは基本的な考え方が共通しており、多少乱暴ですがどれも同じと言うことができますので、要点をまとめます。

## 各アーキテクチャーについて

### Hexagonal Architecture

> ![](/images/Hexagonal-architecture-basic-1.gif)
> 
> 引用: [Hexagonal architecture | Alistair Cockburn](https://alistair.cockburn.us/hexagonal-architecture/)

2005年にAlistair Cockburn氏が公開したアーキテクチャーです。

https://alistair.cockburn.us/hexagonal-architecture/

### Onion Architecture

> ![](/images/image257b0257d255b59255d.png)
> 
> 引用: [The Onion Architecture : part 1 | Programming with Palermo](https://jeffreypalermo.com/2008/07/the-onion-architecture-part-1/)

2008年に[Jeffrey Palermo](https://jeffreypalermo.com/about/)氏が公開したアーキテクチャーです。

https://jeffreypalermo.com/tag/onion-architecture/

### Clean Architecture

> ![](/images/CleanArchitecture.jpg)
> 
> 引用: [The Clean Architecture | The Clean Code Blog](https://blog.cleancoder.com/uncle-bob/2012/08/13/the-clean-architecture.html)

2012年に[Robert C. Martin](http://cleancoder.com/files/about.md)氏が公開したアーキテクチャーです。
Hexagonal Architecture、Onion Architectureなどを参考にしています。

https://blog.cleancoder.com/uncle-bob/2012/08/13/the-clean-architecture.html

## 要点

### 何ができるようにしたいのか？

まず、これらのアーキテクチャーによって何ができるようにしたいのかというと、 __外部の要素に依存せずに実行やテストができるようにしたい__ 、ということになります。

ここでいう外部の要素というのは、UIやフレームワーク、DB、Webサーバーなどのことで、例えばUIであればGUIからCUIに、DBであればMySQLからPostgreSQLに、といった具合に、置き換えが可能な要素、もしくは置き換わることがあり得る要素のことです。

### そのために何をするのか？

そしてそのために何をするのかというと、

1. システムの最も内側に、外部の要素には依存しないビジネスルール用のレイヤーを作る
1. ビジネスルール用のレイヤーの外側に、外部の要素とビジネスルール用のレイヤーを仲介するインターフェイス用のレイヤーを作る

これら２つのレイヤーを作っておくことで、外部の要素が何に置き換わったとしても、ビジネスルール用のレイヤーには何も変更を加えることなく、実行やテストができるようにします。

## 各アーキテクチャーの整理

上記の要点を踏まえて各アーキテクチャーの図や用語を整理すると、以下のようになります。

![](/images/comparison-hexagonal-onion-clean.jpg)

繰り返しになりますが、これらのアーキテクチャーの基本的な考え方は共通しており、Onion ArchitectureやClean Architectureは、Hexagonal Architectureのバリエーションの１つとも言えますので、それぞれのアーキテクチャーは別のものと捉えるのではなく、本質的には同じものだと捉えた方が良いと思っています。
