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

実際にクリーンアーキテクチャを採用して書かれたコードを見て、「これはオニオンアーキテクチャだ」と言うことは可能ですし、逆にオニオンアーキテクチャを採用して書かれたコードを見て、「これはクリーンアーキテクチャではない」と言うことは不可能です。
どのアーキテクチャを採用してもコードに本質的な違いがないのですから、 **すべて同じといって何の問題もありません。**

## 3つのアーキテクチャの要点

![3つのアーキテクチャの要点](/images/clean-onion-hexagonal-same1.png)

todo 続きはここから

## ヘキサゴナルアーキテクチャ

> ![ヘキサゴナルアーキテクチャ](/images/ref-HexagonalArchitecture.gif)
> 
> 出典: [The Hexagonal (Ports & Adapters) Architecture | Alistair Cockburn](https://alistair.cockburn.us/hexagonal-architecture/)

2005年に[Alistair Cockburn](https://alistaircockburn.com/Bio)氏が公開したアーキテクチャです。

https://alistair.cockburn.us/hexagonal-architecture/

(driving) Adapter
(driven) Adapter

## オニオンアーキテクチャ

> ![オニオンアーキテクチャ](/images/ref-OnionArchitecture.png)
> 
> 出典: [The Onion Architecture : part 1 | Programming with Palermo](https://jeffreypalermo.com/2008/07/the-onion-architecture-part-1/)

2008年に[Jeffrey Palermo](https://jeffreypalermo.com/about/)氏が公開したアーキテクチャです。

https://jeffreypalermo.com/2008/07/the-onion-architecture-part-1/

## クリーンアーキテクチャ

> ![クリーンアーキテクチャ](/images/ref-CleanArchitecture.jpg)
> 
> 出典: [The Clean Architecture | The Clean Code Blog](https://blog.cleancoder.com/uncle-bob/2012/08/13/the-clean-architecture.html)

2012年に[Robert C. Martin](https://en.wikipedia.org/wiki/Robert_C._Martin)氏が公開したアーキテクチャです。

https://blog.cleancoder.com/uncle-bob/2012/08/13/the-clean-architecture.html
