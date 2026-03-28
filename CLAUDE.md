# smithy-rs コントリビューション環境

## プロジェクト概要
Smithy IDL から Rust コードを自動生成するコードジェネレータ。AWS SDK for Rust の基盤。
- codegen側: Kotlin/Java（Gradle）
- runtime側: Rust（Cargo）

## AgentTeam

| Agent | 役割 | 起動方法 |
|-------|------|---------|
| tutor | プロジェクト学習・資料生成 | `tutor` エージェントを起動 |
| researcher | issue調査・コード分析・準拠チェック | `researcher` エージェントを起動 |
| coder | 実装・テスト・ビルド | `coder` エージェントを起動 |

## Git運用ルール

### ブランチ戦略
- `origin/main` — 自分のfork。CLAUDE.md, .claude/ 等の個人設定を含む
- 作業ブランチは **`upstream/main` から切る** → PRに個人設定が混ざらない

```bash
# 作業ブランチの作り方
git fetch upstream
git checkout -b fix/issue-XXXX upstream/main
```

### PR提出前チェック（CONTRIBUTING.md準拠）
1. `.changelog/` にエントリを追加
2. rust-runtime/ を変更した場合は Cargo.lock を更新
3. テストが通ること
4. upstream/main の最新を取り込んでいること

## ビルド

詳細は `AGENTS.md` を参照。

```bash
# クライアント側
./gradlew codegen-client-test:assemble --quiet
./gradlew codegen-client-test:test --quiet

# サーバー側
./gradlew codegen-server-test:assemble --quiet
./gradlew codegen-server-test:test --quiet
```

## 学習資料の出力先
Obsidian Vault: `~/Desktop/work/Tech/` 配下に Markdown ノートとして保存する。
