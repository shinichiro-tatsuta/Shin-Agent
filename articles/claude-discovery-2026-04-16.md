---
title: "Claude Code 今日の発見 — 2026-04-16"
emoji: "🔍"
type: "idea"
topics: ["claudecode", "ai", "automation"]
published: true
---

# Claude Code 今日の発見 — 2026-04-16

4月14日のRoutines発表から2日。Claude Codeが「ターミナルの相棒」から「クラウドの同僚」へと変わりつつある週に、面白い事例がいくつも飛び込んできた。

---

## Polymarket自動取引システム、シングルセッションで完成

Örvar Karlssonが、Claude Codeとの一度の会話セッションで、Polymarketの自動トレーディングシステムを構築した。Polymarketとは暗号通貨ベースの予測市場で、選挙結果やイベントの発生可否に賭けることができるプラットフォームだ。

構築したシステムは4つのコンポーネントからなる。価格監視、アービトラージスキャン、取引実行、そして学習ループ。特に興味深いのがNegRiskスキャナーと呼ばれる機能で、複数結果市場において「すべてのYES価格の合計が1ドルにならない」という非効率を検出する。理論上、全てのYESを0.70ドルで購入すれば、結果に関係なく1ドルが保証される。初回スキャンで182件のアービトラージ機会を発見し、8件の取引で75%の勝率、36.2%のROIを達成した。

「確実な情報優位性のない確信買いはやめておけ。つまらない戦略が一番うまくいく」という結論が、トレーディングとAI開発の両方に刺さる。広告運用でも「派手な仮説より地道な改善」という場面は多いはず。

[Medium - Building an Automated Polymarket Trading System](https://medium.com/@rvarkarlsson/building-an-automated-polymarket-trading-system-with-claude-code-1982ff60cc74)

---

## マルチエージェント・コンテンツ工場、月95ドルで稼働中

ある開発者がClaude Codeで、SEO記事生成からReddit投稿、WordPress公開まで一気通貫で行うマルチエージェントシステムを構築した。

アーキテクチャは3層構造。YAMLフロントマター付きMarkdownでワークフローを定義するスキル層、JSONでセッション間の文脈を保持する状態層、そしてPythonでAPI呼び出しやファイル操作を行う実行層。1記事の生成は約25分、ユーザーの手作業は5〜10分程度。

運用費の内訳は、Claude Pro 20ドル、DataForSEO 30ドル、画像生成のfal.ai 5ドルなど、合計月95ドル程度。良い月には「マージン10〜20倍」を達成しているという。仕組み化とコスト管理の参考になる構成だ。コンテンツマーケティングの内製化を検討するなら、この構成をベースに社内向けにアレンジできそう。

[DEV Community - Multi-Agent Content Automation System](https://dev.to/aioperator2026/how-i-built-a-multi-agent-content-automation-system-with-claude-27m8)

---

## 広告分析、3時間→7分の衝撃

Rimoの事例として、営業・マーケティング担当者がClaude Codeで広告分析業務を自動化した話が紹介されていた。

従来の広告分析は、管理画面を開いてキーワードや検索語句を精査して……と、最低3時間、長ければ5時間かかっていた。現在はBigQueryに格納された広告データをClaude Codeが抽出し、状況要約・考察・改善提案まで自動生成する「スキル」を自作。体感で7分まで短縮された。

さらに、Google広告の改善観点を70項目のチェックリストとしてスキル化。「レポート担当・ドキュメント作成に近い役割を代替させている」という表現が印象的だ。YOMIKOの運用レポート業務でも、チェックリストのスキル化は即座に適用できるアプローチ。

[Rimo - 営業・マーケでもここまでできる](https://rimo.app/@rimo/general/claude_code_ad_reporting)

---

## CPOが自分で作った「地味な自動化11個」

アソビュー株式会社のCPO横峯樹氏が、非エンジニアながらClaude Codeで「地味だけど毎日使うAI自動化を11個作った」という記事を公開していた。アソビューはレジャー予約プラットフォームを運営する会社だ。

詳細は記事本文の取得が難しかったが、「毎朝7時に自動実行される仕組み」「デモ映えする一発芸と、業務に定着する仕組みは別物」という方針が語られている。起床してSlackを開く時点で既にAIが動いている、という状態を作っているという。

非エンジニアのCPOが自分で構築しているという点がポイント。「エンジニアに頼まなくても、業務を知っている人が直接自動化を組める」という流れが加速している。

[note - 横峯樹](https://note.com/tyokomine/n/n57e552050ca1)

---

## Agent Teams、「数日が半日になった」

gihyo.jpでClaude Code Agent Teamsの実践記事が公開された。Agent Teamsは、複数のAIエージェントがチームとして協働する機能で、2026年2月にプレビューリリースされた。

従来のサブエージェントは結果のみを報告する構造だったが、Agent Teamsではチームメイト同士が直接メッセージをやり取りし、共有タスクリストで自律的に調整する。有効化は環境変数を設定するだけ。発動も「チームで実装してください」と指示するだけでいい。

実践例として、TypeScriptアプリケーションの非推奨ライブラリ置き換え作業が挙げられていた。「何日もかかったであろう修正が半日〜1日程度ですんだ」とのこと。ただし欠点もあり、トークン消費が通常の約7倍、方向性を誤ると修正が大変、といった点が指摘されている。大規模リファクタリングや新規プロジェクトのキックオフ時に有効か。

[gihyo.jp - Agent Teamsの衝撃と実際](https://gihyo.jp/article/2026/02/get-started-claude-code-07)

---

## Claude Routines登場：ノートPCを閉じたままAIが働く

4月14日、AnthropicがClaude Code Routinesをリサーチプレビューとして公開した。これは「クラウド上で自動実行されるClaude Codeセッション」を作れる機能だ。

構成要素は、プロンプト、リポジトリ、コネクタ（Slack・Linear・GitHubなど）。トリガーはスケジュール（cron）、API、GitHubイベントの3種類。重要なのは、実行がAnthropicのクラウド基盤上で行われる点。つまりノートPCを閉じていても、夜中でも、AIが粛々と作業を進める。

想定ユースケースは、毎日のPR要約、バックログ整理、ドキュメント更新検出、自動コードレビューなど。Routinesの経済性を支えるため、1時間のプロンプトキャッシュも同時に導入された。定型レポートや監視系タスクとの相性は抜群。クライアント向け日次レポートの自動化など、応用範囲は広そう。

[Medium - Anthropic Just Launched Claude Routines](https://medium.com/the-ai-studio/anthropic-just-launched-claude-routines-6430dd721e4a)

---

## Sentry・Notion・楽天、Managed Agentsで本番稼働中

4月8日に公開ベータとなったClaude Managed Agentsを、すでに複数の大企業が本番導入している。Managed Agentsは、AIエージェントをクラウド上で長時間稼働させるためのインフラ基盤だ。

Sentryは、バグを検出するとコードのパッチを自動作成し、プルリクエストを送信するエージェントを稼働させている。Notionは、ワークスペース内で直接タスクをClaudeに委任できる仕組みを構築。楽天は営業・マーケティング・財務向けのエージェントを作り、SlackやTeamsにプラグインしている。

「プロトタイプから本番デプロイまでの期間を10分の1に短縮」とAnthropicは主張している。実際にエンタープライズ規模で動いている事例が複数出てきたことで、「AIエージェントは実験フェーズを超えた」という空気が強まってきた。

[SBbit - Anthropic「Claude Managed Agents」ベータ提供開始](https://www.sbbit.jp/article/cont1/184184)

---

## 今週見つけた小ネタ

**Desktop版の並列セッション対応**：4月14日のアップデートで、Claude Codeデスクトップ版が複数タスクの同時処理に対応した。フロントエンド・バックエンド・PMとターミナルを分けて表示し、3つのClaude Codeに同時に作業させる、という使い方がX上で話題になっていた。

**Monitor tool**：バックグラウンドでログ監視を行い、Claudeが即座に反応できる新ツール。CI/CDのログ監視やサーバーモニタリングと組み合わせる使い方が考えられる。

[Zenn - Claude Code、この1週間で13発](https://zenn.dev/yokoi_ai/articles/cc-2026-04-15)
