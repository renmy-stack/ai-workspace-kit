---
description: 開いているフォルダに標準の作業環境（AGENTS.md / input / output）を整える
---

<!-- Claude Code 用の入口（開発・試験用）。~/.claude/commands/ に置いて使う。
     下の「キットの場所」を、ai-workspace-kit フォルダの絶対パスに書き換えること -->

キットの場所: `{{KIT_DIR}}`

上記キットの `procedures/init-workspace.md` を読み、その手順に従ってください。
案件フォルダは、いま開いているプロジェクトのルート（カレントディレクトリ）です。

## Claude Code だけの追加手順

Claude Code は `AGENTS.md` を自動で読まないため、手順書の「結果を報告する」の前に次を行ってください。

- 案件フォルダに `CLAUDE.md` が**ない**場合: 中身が `@AGENTS.md` の1行だけの `CLAUDE.md` を作る（作成の確認に含まれているものとして扱い、追加の質問はしない）
- `CLAUDE.md` が**ある**場合: 変更しない。`@AGENTS.md` の行がなければ、報告の最後に「CLAUDE.md に `@AGENTS.md` の1行を足すと、共通ルールが自動で読み込まれます」と伝える
- 報告の「作成したもの」に `CLAUDE.md` も含める。また、「共通ルールを読み込むため、Claude Code を再起動するか /clear してください」と添える
