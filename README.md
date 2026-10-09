# ResumeForWebDevelopper

Web系エンジニア向けに、項目入力から履歴書・職務経歴書を作成し、PDF保存できるWebアプリです。転職用ポートフォリオとして開発しています。

現在は仕様策定段階です。以下の技術構成・機能は初期版の採用予定であり、実装済みではありません。

## Overview

本リポジトリでは、Webアプリケーションの開発だけでなく、

- 要件定義
- 設計
- 実装
- テスト
- Git/GitHubによる開発管理
- CI/CD
- 保守・改善

までの開発プロセスを記録します。

## Documentation

- [MVP仕様・必須機能と受け入れ条件](./docs/requirements/mvp.md)
- [ドキュメント一覧](./docs/README.md)
- [Git運用規約](./docs/development/git-conventions.md)
- [Issue記載規則](./docs/development/issue-conventions.md)
- [PR記載規則](./docs/development/pull-request-conventions.md)
- [ファイル命名規則](./docs/development/file-naming-conventions.md)
- [フォルダ命名規則](./docs/development/folder-naming-conventions.md)
- [TypeScript規約](./docs/development/typescript-conventions.md)

## Tech Stack

| 担当 | 採用予定の技術 |
| --- | --- |
| 開発言語 | TypeScript |
| フロントエンド | React・Vite・React Router（SPA） |
| API | Hono・Cloudflare Workers |
| 画面配信 | Cloudflare Workers Static Assets |
| 認証 | Supabase Auth（Googleログイン） |
| DB・認可 | Supabase PostgreSQL・RLS |
| 顔写真保存 | Supabase Storageの非公開領域 |
| PDF保存 | ブラウザ印刷・印刷CSS |

初期版は履歴書・職務経歴書を利用者ごとに各1件、テンプレートを各1種類とします。詳細な範囲と完成基準は[MVP仕様](./docs/requirements/mvp.md)を参照してください。

## Development

アプリの雛形・CIは未作成です。起動・検証手順は実装時に追記します。
