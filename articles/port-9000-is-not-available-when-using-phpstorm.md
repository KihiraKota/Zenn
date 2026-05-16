---
title: "PhpStormを使用中にホストの9000番ポートのポートマッピング設定があるDockerコンテナを立ち上げるとエラーになる"
emoji: "🐳"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: [phpstorm, docker]
published: true
---
## 問題

PhpStormを使用中に、ホストの9000番ポートのポートマッピング設定があるDockerコンテナを立ち上げると、以下のようなエラーが発生します。

```
Error response from daemon: Ports are not available: exposing port TCP 127.0.0.1:9000 -> 0.0.0.0:0: listen tcp 127.0.0.1:9000: bind: An attempt was made to access a socket in a way forbidden by its access permissions.
```

## 原因

PhpStormがXdebug用に9000番ポートを既に使用してるため、9000番ポートが利用できない、という判定になりエラーとなります。

## 解決方法

Dockerコンテナのポートマッピング設定を変更することができない場合は、PhpStormが9000番ポートを使用しないように設定すればよいので、下記のように変更しPhpStormを再起動すると、PhpStormが9000番ポートを使用しないようになります。

設定 > PHP > Debug > Xdebug > Debug port = `9003, 9000` -> `9003`

![](/images/phpstorm-xdebug-por.png)