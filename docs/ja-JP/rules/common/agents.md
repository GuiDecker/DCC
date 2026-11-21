# Agent オーケストレーション

## 利用可能な Agent

ECC の Agent は `ecc@ecc` プラグインに同梱されており、`~/.claude/agents/` には配置されません。
Agent ツールではプラグインスコープの `subagent_type` で呼び出します:

```text
Agent(subagent_type: "dcc:planner", prompt: "...")
```

| Agent | 目的 | 使用タイミング |
|-------|---------|-------------|
| dcc:planner | 実装計画 | 複雑な機能、リファクタリング |
| dcc:architect | システム設計 | アーキテクチャの意思決定 |
| dcc:tdd-guide | テスト駆動開発 | 新機能、バグ修正 |
| dcc:code-reviewer | コードレビュー | コード記述後 |
| dcc:security-reviewer | セキュリティ分析 | コミット前 |
| dcc:build-error-resolver | ビルドエラー修正 | ビルド失敗時 |
| dcc:e2e-runner | E2Eテスト | 重要なユーザーフロー |
| dcc:refactor-cleaner | デッドコードクリーンアップ | コードメンテナンス |
| dcc:doc-updater | ドキュメント | ドキュメント更新 |

全 68 Agent の一覧は `/ecc:ecc-guide` を参照。

## Agent の即座の使用

ユーザープロンプト不要:
1. 複雑な機能リクエスト - **dcc:planner** agent を使用
2. コード作成/変更直後 - **dcc:code-reviewer** agent を使用
3. バグ修正または新機能 - **dcc:tdd-guide** agent を使用
4. アーキテクチャの意思決定 - **dcc:architect** agent を使用

## 並列タスク実行

独立した操作には常に並列 Task 実行を使用してください:

```markdown
# 良い例: 並列実行
3つの agent を並列起動:
1. Agent 1: 認証モジュールのセキュリティ分析
2. Agent 2: キャッシュシステムのパフォーマンスレビュー
3. Agent 3: ユーティリティの型チェック

# 悪い例: 不要な逐次実行
最初に agent 1、次に agent 2、そして agent 3
```

## 多角的分析

複雑な問題には、役割分担したサブ agent を使用:
- 事実レビュー担当
- シニアエンジニア
- セキュリティエキスパート
- 一貫性レビュー担当
- 冗長性チェック担当
