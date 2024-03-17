---
title: "古いバージョンのバグ修正をリリースすることがある場合のGitflowのアレンジ"
emoji: "🦝"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: [git, gitflow]
published: true
---
古いバージョンのバグ修正をリリースすることがあるプロジェクトの場合でも Git のブランチやタグが複雑にならないように、 Gitflow をアレンジして使っているブランチモデル(aka.ブランチ戦略)についての説明です。

# Gitflow について

[Vincent Driessen](https://nvie.com/about/) 氏が [A successful Git branching model](https://nvie.com/posts/a-successful-git-branching-model/) にて公開した Git のブランチモデルのことです。

> ![](/images/git-model@2x.png)
> 
> 引用元: [A successful Git branching model](https://nvie.com/posts/a-successful-git-branching-model/)

# 解決したい問題

常に最新のバージョンだけをリリースするプロジェクトであれば Gitflow のブランチモデルで特に問題はないのですが、以下のようなことがある場合、

1. ver.1.0 をリリース
1. ver.2.0 をリリース
1. ver.1.0 でバグが見つかり、バグ修正版の ver.1.1 をリリースする必要がある

ver.1.1 を Gitflow のブランチモデルではどう扱うべきなのか、人によって意見が分かれるかと思います。

例えば、

- ver.1.0 のタグから作成した hotfix ブランチに ver.1.1 のタグを追加する
- 古いバージョンのサポート用のブランチを作成する

などの方法も考えられるかと思います。

# 解決策

上記の問題を解決するために Gitflow をアレンジしたブランチモデルが以下のものです。

![](/images/Gitflow-arrange.jpg)

1. main ブランチから develop ブランチを作成する
1. develop ブランチから feature ブランチを作成して機能の開発などを進め、完了したら develop ブランチにマージする
1. develop ブランチから release/1.x ブランチを作成してリリースに必要な作業を進める
1. __release/1.x ブランチでバグが見つかった場合は、 release/1.x ブランチから bugfix ブランチを作成し、修正が完了したら release/1.x ブランチにマージする__
1. __リリースに必要な作業、バグ修正の完了後、 release/1.x ブランチにタグを追加してリリースする__
1. リリースの完了後、 release/1.x ブランチを develop ブランチと main ブランチにマージする
1. 新しいバージョンをリリースする場合は、 3～6 と同様の作業を release/2.x のブランチで進める
1. 古いバージョンでバグが見つかった場合は、 4～5 と同様の作業を release/1.x のブランチで進める
1. __古いバージョンのバグ修正のリリース完了後、release/1.x ブランチを release/2.x ブランチにマージする__
1. 5～6 と同様の作業を release/2.x ブランチで進める

※ __太字__ になっている箇所が Gitflow からアレンジした箇所です

# 最後に

標準的な Gitflow ではなく、あくまでも Gitflow のアレンジ版だということに注意してください。
