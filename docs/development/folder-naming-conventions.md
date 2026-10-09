# Folder Naming Conventions

関連するファイルの置き場所を予測しやすくする。命名規則と構成例を区別し、使用しない空フォルダを先に作らない。

## 基本ルール

- 原則、小文字のkebab-caseを使う。例：`resume-editor`、`career-history`。
- 半角英数字・ハイフンを使い、空白・日本語・意味のない略語を避ける。
- 同じ意味の語を統一する。履歴書は`resume`、職務経歴書は`career-history`を基本とする。
- 機能は単数形、複数の同種ファイルをまとめる分類は複数形を基本とする。例：`features/resume`、`components`、`routes`。
- `src`、`public`、`docs`、`dist`、`.github`、`node_modules`など、慣例・ツールが使用する名前は維持する。
- 大文字小文字だけ異なるフォルダを作らず、importや文書リンクの表記を一致させる。
- `common`、`misc`、`temp`へ雑多な処理を集めず、役割・機能を明確にする。

## 今後の構成例

下表は雛形設計時の候補。実際のフロントエンド・APIのルート配置は、ビルドとWorkers構成を確認して決める。

| ルートからの例 | 役割 |
| --- | --- |
| `docs/requirements` | MVP・要件 |
| `docs/development` | 開発規約・進捗 |
| `docs/design` | API・DB・認証等の設計 |
| `src/features/resume` | 履歴書に固有の画面・Hook・処理 |
| `src/features/career-history` | 職務経歴書に固有の画面・処理 |
| `src/components` | 複数機能で使う画面部品 |
| `src/lib` | 外部サービスとの接続・共通基盤 |
| `server/routes` | Hono APIのルート |
| `server/middleware` | APIの共通前処理 |
| `supabase/migrations` | DB・RLSの変更履歴（導入時） |

## 配置の判断

- 特定機能だけが使うファイルは、その機能の近くへ置く。
- 共通化は複数の実際の利用先ができてから行う。将来用に抽象層を増やさない。
- 単体テストは対象の隣、E2Eテストは導入時に専用フォルダへ置く。
- フォルダの分割は責務が分かれたときに行い、最初から深い階層にしない。
- 生成物・依存パッケージはGitへ登録しない。例外の生成コードが必要なら、理由と再生成手順を記録する。
- 既存フォルダの移動はimport・設定・リンクへの影響を確認し、機能変更と無関係な大規模移動を同じPRへ入れない。
