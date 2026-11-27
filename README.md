# ai-workspace-kit（試作版）

AIエージェント初心者でも、標準のフォルダ構成とルールに沿って仕事ができるようにするためのキットです。
**ルールを覚えるのではなく、ルールに沿った環境の中で仕事をする**ことを目指しています。

> 試作版です。AGENTS.md と instruction.md の中身はたたき台で、仮想秘書（`.company/`）はまだ組み込んでいません。

## 準備（最初に1回だけ）

1. このキット（ai-workspace-kit フォルダ）を GitHub から取得する
2. `install/copilot/init-workspace.prompt.md` を、VS Code の**ユーザープロンプトフォルダ**にコピーする
   - Copilot Chat の歯車（Configure Chat）→「Prompt Files」→ ユーザーデータフォルダ を選ぶと開ける
3. コピーしたファイルの `{{KIT_DIR}}` を、手順1のフォルダの絶対パスに書き換える（例: `C:\tools\ai-workspace-kit`）

## 使い方（案件ごと）

1. VS Code で**案件フォルダを開く**（例: `C:\work\案件A`）
2. Copilot Chat を **Agent モード**にして、`/init-workspace` と入力する
3. 「このフォルダに作業環境を作ってもいいですか？」に「はい」と答える

初期化後の案件フォルダ:

```
案件A/
├── AGENTS.md          … AIと人間の共通ルール（Copilot が自動で読む）
├── .company/          … 仮想秘書（今後組み込み予定）
├── input/             … 参照資料（置き方は自由。中身は変更しない）
└── output/            … 成果物と、その作り方
    └── _template/     … 成果物フォルダのひな形（instruction.md + work/）
```

各フォルダの `README.md` に使い方が書いてあります。

## キットの構成

| パス | 役割 |
|---|---|
| `workspace-template/` | 案件フォルダの**正本**。初期化ではここから不足分だけコピーする |
| `procedures/init-workspace.md` | 初期化手順の本文（Copilot / Claude Code 共通） |
| `install/copilot/` | Copilot 用の入口（ユーザープロンプトフォルダに置く） |
| `install/claude-code/` | Claude Code 用の入口（開発・試験用。`~/.claude/commands/` に置く） |
| `.github/prompts/integrate-kit.prompt.md` | 会社の仮想秘書に組み込むための引き継ぎプロンプト（`/integrate-kit`） |

標準構成を変えたいときは `workspace-template/` を直します。手順を変えたいときは `procedures/init-workspace.md` を直します。

## Claude Code で試すとき（開発者向け）

- `install/claude-code/init-workspace.md` を `~/.claude/commands/` にコピーし、`{{KIT_DIR}}` を書き換える
- 案件フォルダで `claude` を起動し、`/init-workspace` を実行する
- Claude Code は `AGENTS.md` を自動で読まないため、試すときは案件フォルダの `CLAUDE.md` に `@AGENTS.md` の1行を書いて読み込ませる（試験用。配布物には含めない）

## 会社側で完成させること

このキットは GitHub に置き、会社で取得して、会社の GitHub Copilot で仕上げる。

**始め方**: 会社の VS Code でこの ai-workspace-kit フォルダを開き、Copilot Chat（Agent モード）で `/integrate-kit` と入力する。
引き継ぎ内容と手順は `.github/prompts/integrate-kit.prompt.md` に書いてある（Copilot 以外で使うときは、このファイルの本文を貼り付ければよい）。

### input/ の整理方針（方針は決定済み、中身は会社で記入）

- **方針**: `input/` は自由に置ける（固定のサブフォルダは作らない）。利用者が自分で作った構成は尊重する。直下に散らかったとき・頼まれたときだけ AI が整理を提案し、承認を得てから移動する
- **整理の基準**: 会社でいつも使っているフォルダ構成を、`workspace-template/input/README.md` の「整理の参考にするフォルダ構成」に書く（現在は未記入）

### 仮想秘書（Copilot 版）との統合

- **方針**: `.company/` は input/・output/ と同じ階層（案件フォルダ直下）に作る
- **方針**: 会社の Copilot 版 `/company` の「`.company` フォルダを作っていいですか？」の確認に、作業環境の作成をまとめる（質問は1回のまま）
  - 例:「このフォルダに仮想秘書（.company）と作業環境（AGENTS.md / input / output）を作ってもいいですか？」
  - 承認後の処理は `procedures/init-workspace.md` の手順3以降をそのまま使う
- `/init-workspace` は、作業環境だけを足し直したいとき用に残す

## 未確定・要確認

- [ ] 会社の標準フォルダ構成を `workspace-template/input/README.md` に記入
- [ ] Copilot の版によるプロンプトファイルの書式（`agent: agent` か、旧書式の `mode: agent` か）
- [ ] Copilot のユーザープロンプトから、ワークスペース外（キット）のファイルを読めるか
- [ ] AGENTS.md・instruction.md の内容確定
- [ ] 仮想秘書（Copilot 版）への組み込み
