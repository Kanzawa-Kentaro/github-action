# GitHub Actions イベント一覧メモ

以下は、指定されたイベントが「いつ発火するか」と「何に使うか」の要点です。


| Event                         | いつ発火するか                             | 主な用途 / メモ                                                         |
| ----------------------------- | ----------------------------------- | ----------------------------------------------------------------- |
| `branch_protection_rule`      | ブランチ保護ルールを作成・変更・削除したとき              | 保護ルール変更の監査、通知                                                     |
| `issues`                      | Issue の作成・編集・クローズなど                 | Issue 運用自動化、ラベル付け                                                 |
| `pull_request_review_comment` | PR の差分行にレビューコメントが付いたとき              | レビュー補助、Bot 応答                                                     |
| `check_run`                   | Check Run（CI チェック単位）の状態変化時          | 外部 CI 連携、結果通知                                                     |
| `label`                       | ラベルの作成・編集・削除時                       | ラベル管理の同期、監査                                                       |
| `pull_request_target`         | PR を対象に、**ベースリポジトリ文脈**で動く           | フォーク PR でもシークレットを扱えるが安全設計必須                                       |
| `check_suite`                 | Check Suite（複数チェックのまとまり）の状態変化時      | チェック群の統合処理                                                        |
| `merge_group`                 | Merge Queue（マージキュー）で検証が走るとき         | キュー向け CI                                                          |
| `push`                        | ブランチ/タグへの push 時                    | 最も基本の CI/CD トリガー                                                  |
| `create`                      | ブランチ/タグが作成されたとき                     | 初期化処理、通知                                                          |
| `milestone`                   | マイルストーンの作成・編集・クローズ時                 | リリース運用補助                                                          |
| `registry_package`            | GitHub Packages の publish/update 時  | パッケージ公開後処理                                                        |
| `delete`                      | ブランチ/タグが削除されたとき                     | クリーンアップ、通知                                                        |
| `page_build`                  | GitHub Pages のビルド時                  | Pages 公開パイプライン監視                                                  |
| `release`                     | Release の作成・公開・編集時                  | 配布物生成、公開通知                                                        |
| `deployment`                  | Deployment が作成されたとき                 | デプロイ開始フロー                                                         |
| `project`                     | Projects (classic) の変更時             | classic Project 自動化（新 Projects とは別）                               |
| `repository_dispatch`         | API で `repository_dispatch` を送信したとき | 外部システムから手動トリガー                                                    |
| `deployment_status`           | Deployment 状態が更新されたとき               | デプロイ成功/失敗通知、後続処理                                                  |
| `project_card`                | Projects (classic) のカード変更時          | classic Project カード自動化                                            |
| `schedule`                    | cron 指定時刻                           | 定期バッチ、夜間ジョブ                                                       |
| `discussion`                  | Discussion の作成・編集・クローズ時             | コミュニティ運用自動化                                                       |
| `project_column`              | Projects (classic) のカラム変更時          | classic Project カラム連動                                             |
| `status`                      | Commit Status が更新されたとき              | 古い status API 連携の監視                                               |
| `discussion_comment`          | Discussion コメント作成・編集時               | コメント監視、Bot 応答                                                     |
| `public`                      | リポジトリを public に変更したとき               | 可視性変更の監査通知                                                        |
| `watch`                       | リポジトリが star されたとき                   | Star 通知、分析                                                        |
| `fork`                        | リポジトリが fork されたとき                   | Fork 通知、分析                                                        |
| `pull_request`                | PR の作成・同期・クローズなど                    | PR CI の基本                                                         |
| `workflow_call`               | 他ワークフローから reusable workflow が呼ばれたとき | 共通ワークフロー部品化                                                       |
| `gollum`                      | Wiki ページが更新されたとき                    | Wiki 更新通知                                                         |
| `pull_request_comment`        | PR コメント時を意図した名称                     | GitHub Actions の `on` では通常使わず、PR コメント監視は `issue_comment` を使うのが一般的 |
| `workflow_dispatch`           | UI/API から手動実行したとき                   | 手動運用、パラメータ付き実行                                                    |
| `issue_comment`               | Issue/PR へのコメント作成・編集時               | `/command` 形式の ChatOps                                            |
| `pull_request_review`         | PR レビュー提出・編集時                       | 承認/却下を契機に処理                                                       |
| `workflow_run`                | 別ワークフローの完了時                         | ワークフロー間の連鎖実行                                                      |


## 補足

- PR に対する「コメント」を拾いたい場合は、用途で使い分けます。  
  - レビューの差分行コメント: `pull_request_review_comment`  
  - PR 会話タブのコメント: `issue_comment`（PR も Issue と同じコメントイベントに乗る）
- `project` / `project_card` / `project_column` は Projects (classic) 向けです。

