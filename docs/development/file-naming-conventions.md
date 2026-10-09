# File Naming Conventions

名前から役割が分かり、OS間で表記が揺れないことを目的とする。本規則は新規ファイルに適用し、既存ファイルは必要な変更の際に整える。

## 命名一覧

| 対象 | 規則 | 例 |
| --- | --- | --- |
| Reactコンポーネント・ページ | PascalCase＋`.tsx` | `ResumeForm.tsx`、`ResumePage.tsx` |
| カスタムHook | `use-`から始まるkebab-case＋`.ts` | `use-resume.ts`（関数名は`useResume`） |
| その他のTypeScript | kebab-case＋`.ts` | `resume-api.ts`、`validate-resume.ts` |
| 型・入力スキーマ | 対象を示すkebab-case | `resume-types.ts`、`resume-schema.ts` |
| 単体・結合テスト | 対象名＋`.test.ts`／`.test.tsx` | `validate-resume.test.ts`、`ResumeForm.test.tsx` |
| E2Eテスト（導入時） | シナリオ名＋`.spec.ts` | `resume-export.spec.ts` |
| CSS | kebab-case＋`.css` | `print.css`、`resume-preview.css` |
| CSS Modules（採用時） | コンポーネント名＋`.module.css` | `ResumeForm.module.css` |
| Markdown | kebab-case＋`.md` | `issue-conventions.md`、`mvp.md` |
| 静的画像 | 内容を示すkebab-case | `resume-sample.png` |

PascalCaseは各単語の先頭を大文字にする形式、kebab-caseは小文字の単語をハイフンでつなぐ形式。テストの拡張子は命名案であり、テストライブラリを決定済みとするものではない。

## 具体的なルール

- 半角英数字・ハイフンを基本とし、空白・日本語・`final`・`new`・`copy`などの状態名を避ける。
- `file.ts`、`data.ts`、`utils.ts`のような広すぎる名前より、対象を示す名前を使う。
- `.tsx`はJSXを含むファイル、`.ts`はJSXを含まないファイルに使う。
- ファイル名とimportパスは大文字・小文字まで一致させる。大文字小文字だけ異なるファイルを作らない。
- `README.md`、`LICENSE`、`.gitignore`、`package.json`、`tsconfig.json`などの慣例名・ツールが要求する名前は維持する。
- 生成ファイルは生成ツールの名前を維持し、手作業で命名規則へ合わせない。
- `index.ts`は明確な入口だけに使い、全フォルダへの一括追加・無制限な再exportを避ける。
- 履歴書用のアップロード写真はこの静的ファイル規則とは別。元の氏名・ファイル名を公開パスへ使わず、保存先識別子は写真処理の設計で定める。

Markdownの既存規約名は `*-conventions.md` にそろえる。ロードマップなど日付が役割に必要な文書は `portfolio-roadmap-2026-10-25.md` のようにISO形式の日付を使用する。
