# TypeScript Conventions

React画面とHono APIで使う規則。可読性・型安全性・変更のしやすさを優先する。ライブラリの選定やLint・整形の自動化は、雛形作成で実装する。本文書の作成時点では未導入。

## 命名・書式

| 対象 | 規則 | 例 |
| --- | --- | --- |
| 変数・関数 | camelCase | `resumeId`、`saveResume` |
| Reactコンポーネント・型・interface | PascalCase | `ResumeForm`、`ResumeInput` |
| Hook | `use`＋PascalCase | `useResume` |
| 真偽値 | 状態や問いが分かる名前 | `isSaving`、`hasPhoto`、`canSubmit` |
| 固定の設定定数 | UPPER_SNAKE_CASE | `MAX_PHOTO_SIZE_BYTES` |
| 通常のconst変数 | camelCase | `const resume = ...` |

- インデント2スペース、セミコロンあり、文字列はダブルクォート、複数行の末尾カンマを基本とする。
- ファイル末尾に改行を入れる。整形ツール導入後はその設定を優先し、手作業の整形議論を減らす。
- 再代入しない値は`const`、再代入が必要な値だけ`let`。`var`は使わない。
- 比較は原則`===`／`!==`。複雑な三項演算子・深いネストは分岐や小さい関数へ分ける。
- ファイル・フォルダ名は[ファイル規則](./file-naming-conventions.md)・[フォルダ規則](./folder-naming-conventions.md)を参照する。

## 型の扱い

- 自作コードは`strict: true`で型チェックする。フロントエンド・API双方で適用する。
- 明示的な`any`を原則使わない。外部入力やcatchの値は`unknown`として受け、検証・絞り込みで型を確定する。
- ローカル変数は型推論を活用する。外部へ公開する関数やAPI境界は、引数・戻り値の契約を明確にする。
- オブジェクトの通常の型、unionは`type`を基本とする。拡張が必要な契約やライブラリ連携では`interface`を使ってよい。`IResume`のような接頭辞は不要。
- 状態は文字列リテラルのunionを優先し、数値・文字列の意味をコードで表す。
- `as`による強制変換、非nullアサーション`!`、`@ts-ignore`で検証を省略しない。必要な例外は根拠と影響をPRへ記録する。
- `as const`など値から型を狭める表現は許可する。型を偽るための`as unknown as ...`を使わない。
- `null`は「明示的に値がない」、`undefined`は「未指定」を基本とし、API・DBの契約に合わせる。

```ts
type SaveState = "idle" | "saving" | "saved" | "error";

function getErrorMessage(error: unknown): string {
  return error instanceof Error ? error.message : "処理に失敗しました";
}
```

このエラー例は型の絞り込み用。APIの内部エラー本文をそのまま利用者へ返す用途では使わない。

## 入力・API・認可

- TypeScriptの型だけで外部入力が正しいと判断しない。HTTP本文・DBから扱うデータ・ファイル等は、境界で必要な実行時検証を行う。
- 画面とAPIの両方で入力を検証する。共通化できる制約は共有し、サーバー側の認可は画面の検証とは別に行う。
- `await request.json() as ResumeInput`のような型アサーションだけで入力を確定しない。
- 所有者IDは検証した認証情報から取得し、本文から受け取ったIDを信用しない。
- DB・Storageは本人のアクセス制限を維持し、通常CRUDで管理者キーを使ってRLSを迂回しない。
- 入力検証ライブラリと写真の上限値は未決定。決定時はMVP仕様・画面・API・保存先を整合させる。

## 関数・モジュール・非同期処理

- 1つの関数は1つの責務を基本とし、固定の行数上限は設けない。
- 関数宣言とアロー関数は役割に応じて使う。単純な関数は宣言、コールバックはアローを基本とし、既存コードの一貫性を保つ。
- 自作モジュールはnamed exportを基本とする。ツールが要求するdefault exportは許可する。
- 型のみのimportは`import type`を使用する。フロントエンドからサーバーの秘密情報を持つモジュールをimportしない。
- Promiseは`await`、返却、または失敗処理を持つ明示的なバックグラウンド処理として扱う。`void`だけで失敗を放置しない。
- 非同期の保存結果は確認してから成功表示する。catchを空にしたり、失敗時に成功値を返したりしない。
- DB・Storageの複数操作は途中失敗を前提にし、旧写真の保護と削除の再試行を設計する。

## Reactの規則

- 関数コンポーネントとHookを使う。Hookはコンポーネント・カスタムHookのトップレベルで呼ぶ。
- state・propsを直接変更せず、新しい値を作って更新する。
- 描画に使う派生値は、不要に重複したstateへ保存しない。
- 繰り返し描画のkeyは安定したIDを使う。追加・削除可能なプロジェクトのkeyに配列indexを使わない。
- 保存中・成功・失敗・未保存を区別し、認証切れ・ログアウト時の個人データをクリアする。
- ラベル・キーボード操作・エラー表示は入力機能と一緒に実装する。
- ユーザー入力の表示は通常のテキスト描画を基本とし、HTMLとして直接挿入しない。

## コメント・ログ・確認

- コメントは「なぜその処理が必要か」を記録する。処理を読み直しただけの説明は増やさない。
- TODOは対応するIssueや条件を示す。未完了のTODOを含む機能を完了済みとしない。
- トークン、秘密キー、書類本文、写真、利用者の個人情報をログへ出さない。
- 認可・入力検証・差し替え等の重要な処理は、成功だけでなく失敗ケースを検証する。
- 導入後のPRではLint・型チェック・Build・変更に関係するテストを確認する。未導入の検査を成功済みとして記録しない。

## 参考

- [strict（TypeScript公式）](https://www.typescriptlang.org/tsconfig/strict.html)
- [型の絞り込み（TypeScript公式）](https://www.typescriptlang.org/docs/handbook/2/narrowing.html)
