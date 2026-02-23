# public-skills

OpenClaw 用の **公開 AgentSkills リポジトリ**です。  
ここには、再利用できるスキル（`SKILL.md` + 必要な補助ファイル）を置きます。

## Purpose

- 使い回せる skill をまとめる
- 他環境へ配布しやすくする
- スキルを公開前提で整理する

## ⚠️ Security Rules (Important)

このリポジトリは **public** です。必ず守ってください。

- APIキー / トークン / パスワード / 個人情報を置かない
- `.env` や credential ファイルをコミットしない
- 実在ID・内部URL・秘密情報をサンプルに含めない
- 公開して問題ない内容か、push 前に必ず確認する

## Skill Structure

各 skill は 1 フォルダ単位で管理します。

```text
<skill-name>/
├── SKILL.md                 # required
├── scripts/                 # optional
├── references/              # optional
└── assets/                  # optional
```

### Naming

- フォルダ名は `lowercase-hyphen` 推奨（例: `weather-alert`, `notion-sync`）
- 1 skill = 1 directory

## Quick Start

```bash
# clone
git clone https://github.com/RYO1223/skills.git
cd skills

# 新しい skill を追加
mkdir my-skill
# my-skill/SKILL.md を作成
```

## Commit Checklist

push 前にこれだけ確認:

- [ ] `SKILL.md` がある
- [ ] 不要ファイル（tmp, cache, local logs）がない
- [ ] 機密情報が含まれていない
- [ ] 公開して問題ない説明文になっている

## Notes

- この repo は「公開・配布用」の置き場
- 実験中のラフな内容はローカルで磨いてから移植する
