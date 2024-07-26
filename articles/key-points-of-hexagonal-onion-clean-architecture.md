Hexagonal, Onion, Clean Architectureの超ザックリとした要点


クリーンアーキテクチャから見たオニオンアーキテクチャ

Hexagonal Architectureの

Hexagonal Architecture
Onion Architecture
Clean Architecture

Aから見たBとC
B and C as seen from A


---

ヘキサゴナルアーキテクチャ 別名:ポートアンドアダプターアーキテクチャ

原文 https://alistair.cockburn.us/hexagonal-architecture/
日本語訳 https://blog.tai2.net/hexagonal_architexture.html

内
アプリケーション
ポート
アダプター (GUI)
外

オニオンアーキテクチャ

原文 https://jeffreypalermo.com/tag/onion-architecture/

内
Domain Model
Domain Services (リポジトリインターフェイス)
Application Services
※↑アプリケーションコア
User Interfaces(コントローラー), Infrastructure, Tests
外

クリーンアーキテクチャ

原文 https://blog.cleancoder.com/uncle-bob/2012/08/13/the-clean-architecture.html
日本語訳 https://blog.tai2.net/the_clean_architecture.html

内
エンタープライズビジネスルール (エンティティ)
アプリケーションビジネスルール (ユースケース)
インターフェイスアダプター (Controllers, Gateways, Presenters)
フレームワーク&ドライバー (Devices, Web, DB, External Interfaces, UI)
外