---
title: "PhpStormでPrettierのコードフォーマットを実行する"
emoji: "🦝"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: [phpstorm, prettier]
published: true
---
PhpStormでPrettierのコードフォーマットを実行するための設定です。

## 設定

### 1. プラグインをインストールする

Prettierのプラグインをインストールし、有効にしてください。

![](/images/phpstorm-prettier1.png)

### 2. Prettierをインストールする

以下のコマンドをターミナルで実行するなどの方法で、Prettierをインストールしてください。

```
$ npm install --save-dev prettier
```

### 3. Prettierの機能を有効にする

「Automatic Prettier configuration」または「Manual Prettier configuration」を選択し、Prettierの機能を有効にしてください。

![](/images/phpstorm-prettier2.png)

有効にすると、右クリックメニューから「Reformat with Prettier」が選択できるようになります。

![](/images/phpstorm-prettier3.png)

## 参考資料

- https://prettier.io/docs/webstorm
- https://www.jetbrains.com/help/webstorm/prettier.html
