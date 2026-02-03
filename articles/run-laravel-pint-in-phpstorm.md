---
title: "PhpStormでDockerコンテナにあるLaravel Pintのコードフォーマットを実行する"
emoji: "🦝"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: [phpstorm, laravelpint]
published: false
---
PhpStormで、Dockerコンテナの中にあるLaravel Pintを使って、コードフォーマットを実行したい、という場合の設定手順です。
ローカルのアプリケーション実行環境をDockerで構築し、その上で開発を行っている、という開発環境を想定しています。

また、設定手順は以下の環境で行ったものです。

- Windows 11 Pro
- PhpStorm 2025.3.2
- Docker Desktop 4.41.2 (※「Use the WSL 2 based engine」をON)

## 設定手順

## 参考資料

- https://pleiades.io/help/phpstorm/docker.html
- https://pleiades.io/help/phpstorm/configuring-remote-interpreters.html#remote-interpreter-docker-compose
- https://pleiades.io/help/phpstorm/using-laravel-pint.html
