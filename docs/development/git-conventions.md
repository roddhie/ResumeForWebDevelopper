# Git Conventions

## Commit Message

本プロジェクトでは、コミットメッセージに
[Conventional Commits](https://www.conventionalcommits.org/) の形式を採用します。

### Format

```text
<type>: <description>

```

| Type       | Description | Example                           |
| ---------- | ----------- | --------------------------------- |
| `feat`     | 新機能         | `feat: add resume registration`   |
| `fix`      | バグ修正        | `fix: fix resume validation`      |
| `docs`     | ドキュメント変更    | `docs: add requirements document` |
| `test`     | テスト追加・修正    | `test: add resume tests`          |
| `refactor` | リファクタリング    | `refactor: improve resume form`   |
| `ci`       | CI/CD関連     | `ci: add GitHub Actions workflow` |
| `chore`    | その他の変更      | `chore: update dependencies`      |

Issue・PRの記載方法とブランチ運用は、[Issue規則](./issue-conventions.md)・[PR規則](./pull-request-conventions.md)を参照してください。
