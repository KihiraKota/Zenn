---
title: "PhpStormでDockerコンテナのPHPを使ってLaravel Pintのコードフォーマットを実行する"
emoji: "🦝"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: [phpstorm, laravelpint]
published: true
---
Dockerコンテナの中にあるPHPを使ってLaravel Pintのコードフォーマットを実行するためのPhpStormの設定です。

設定は以下の環境で行っています。

- Windows 11 Pro
- PhpStorm 2025.3.2
- Docker Desktop 4.41.2 (※「Use the WSL 2 based engine」をON)
- WSL上にPhpStormのプロジェクトがある
- Docker ComposeでPHP環境があるDockerコンテナを使用している

## 設定

### 1. PhpStormからDockerに接続する

まずは、PhpStormからDockerに接続できるようにします。

PhpStormのDockerプラグインが有効になっていることを確認してください。

Settings > Plugins > Installed と進み、「docker」で検索すると、Dockerプラグインが有効になっていることを確認できます。
Dockerプラグインが有効になっていない場合は、チェックボックスをONにして、有効化してください。

![](/images/phpstorm-laravel-pint1.png)

Settings > Build, Execution, Deployment > Docker と進み、左上の「＋」から、Dockerとの接続設定を追加してください。

「Connect to Docker daemon with:」は、「Docker for Windows」を選択してください。

![](/images/phpstorm-laravel-pint2.png)

Dockerとの接続設定の追加が完了すると、「Services」のツールウィンドウに、追加したDockerとの接続設定が表示されます。
「Docker Desktop」が起動している状態であれば、 右クリック > Connect を選択すると、Dockerに接続し、作成済みのコンテナなどが表示されます。

![](/images/phpstorm-laravel-pint3.png)

### 2. PhpStormからDockerのPHPを実行する

次に、Dockerのコンテナの中にある `php` コマンドを実行できるようにします。

Settings > PHP と進み、「CLI Interpreter:」の右にある「...」のボタンを押してください。

![](/images/phpstorm-laravel-pint4.png)

表示されたウィンドウの左上にある「＋」を押し、「From Docker, Vagrant, VM, WSL, Remote...」を選択してください。

![](/images/phpstorm-laravel-pint5.png)

「Docker Compose」を選択してください。

「Configuration files:」で、プロジェクトで使用しているComposeファイルを選択してください。

「Configuration files:」の選択に間違いがなければ、「Services:」にプロジェクトで使用しているDockerのサービス(=コンテナ)の一覧が表示されるので、PHP環境があるサービスを選択してください。

Composeファイルが .env ファイルの値を参照している場合は、「Environment variables:」の右にある「🗒️(ノートのようなアイコン)」のボタンから、 .env ファイルの値を追加してください。

![](/images/phpstorm-laravel-pint6.png)

上記の設定完了後、 `php` コマンドを実行できるようになっている場合は、PHPのバージョンが表示されます。

![](/images/phpstorm-laravel-pint7.png)

### 3. PhpStormのコードフォーマットをLaravel Pintに切り替える

最後に、PhpStormのコードフォーマットをLaravel Pintに切り替えます。

Settings > PHP > Quality Tools > Laravel Pint と進み、「Configuration:」の右にある「...」のボタンを押してください。

表示されたウィンドウの左上にある「＋」を押してください。

「CLI Interpreter:」の右にある「...」のボタンから、「[2. PhpStormからDockerのPHPを実行する](#2.-phpstorm%E3%81%8B%E3%82%89docker%E3%81%AEphp%E3%82%92%E5%AE%9F%E8%A1%8C%E3%81%99%E3%82%8B)」で追加した「CLI Interpreter」を選択してください。

「Laravel Pint path:」に、プロジェクトで使用しているLaravel Pintの実行ファイルのパスを入力してください。

:::message
入力するパスは、PHP環境があるコンテナ上の絶対パスにする必要があることに注意してください。
:::

「Laravel Pint path:」の入力完了後、「Validate」のボタンを押し、Laravel Pintが実行できることを確認してください。

![](/images/phpstorm-laravel-pint8.png)

「Options:」の「Path to pint.json:」で、プロジェクトで使用しているLaravel Pintの設定ファイルを選択してください。

「Ruleset:」は、「defined in pint.json」を選択してください。

![](/images/phpstorm-laravel-pint9.png)

 Settings > PHP > Quality Tools と進み、「Laravel Pint」を選択すれば設定完了です。
「Ctrl + Alt + L」のショートカットなどで、「Laravel Pint」のコードフォーマットを実行することができます。

![](/images/phpstorm-laravel-pint10.png)

## 参考資料

- https://pleiades.io/help/phpstorm/docker.html
- https://pleiades.io/help/phpstorm/configuring-remote-interpreters.html#remote-interpreter-docker-compose
- https://pleiades.io/help/phpstorm/using-laravel-pint.html
