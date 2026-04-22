---
title: "Claude Code 今日の発見 — 2026-04-22"
emoji: "🔍"
type: "idea"
topics: ["claudecode", "ai", "automation"]
published: true
---

# Claude Code 今日の発見 — 2026-04-22

「自動化は完璧を目指さない」が今週のキーワードかもしれない。24時間稼働の基盤が整いつつある一方で、実務で成果を出している人たちは「一番面倒な部分だけ」を狙い撃ちしている。

---

## QAエンジニアがテスト実行時間を74%削減、年間68時間を取り戻した話

エムスリーのQAエンジニア今井氏が、Claude Codeを6ヶ月間使い倒した結果をテックブログで公開した。E2Eテストの実行時間が105分から27分へ、74%の短縮。年間に換算すると68時間分のCI/CD待ち時間が消えた計算になる。

ポイントは「固定wait時間の撲滅」だった。従来のテストコードは「3秒待つ」のような決め打ちが散らばっていたが、Claude Codeに「完了したら次へ進む」条件ベースの待機処理へ書き換えさせた。Playwrightの`waitForResponse`や`waitForLoadState`を適切に使い分けるリファクタリングを、AIが淡々とこなした。

もうひとつの成果は、MCP（Model Context Protocol）でConfluenceやJIRAと接続し、テスト結果からドキュメント更新までを一気通貫で自動化したこと。コード貢献数が16件から67件へ、3.2倍に増えたという数字が、AIとの協働が「量」にも効くことを示している。広告運用のレポーティング自動化でも、この「テスト→ドキュメント更新」の一気通貫パターンは応用できそうだ。

[エムスリーテックブログ](https://www.m3tech.blog/entry/2026/04/20/090035)

---

## 「完全自動化を目指さない」— AWS AI Heroの割り切り方

AWS AI Heroでもあるみのるん365氏が、日常業務の自動化11個を公開した。経費精算、稼働報告、プレゼン資料作成、メール監視など。

印象的なのは「半自動化」という割り切りだ。経費精算の例では、MoneyForward→Gmail→freeeという手作業フローのうち、「freeeへの手入力」だけは残している。完全自動化すると例外処理が複雑になりすぎるため、「一番面倒な照合作業」だけをClaude Codeに任せた。結果、30分の作業が5〜10分に短縮された。

プレゼン資料作成では、会議メモをMarp（Markdownスライド）形式で構造化し、PDF/PPTXに変換する流れを組んでいる。デザインの統一性を維持しながら、中身の作成に集中できる。クライアント向け提案資料の大量生成にも使えるパターンだ。

[Qiita - みのるん365](https://qiita.com/minorun365/items/114f53def8cb0db60f47)

---

## ノートパソコンを閉じてもAIが働き続ける — Claude Routinesがローンチ

4月14日、AnthropicがClaude Code向けに「Routines」をリリースした。プロンプト、リポジトリ、外部ツール（GitHub、Slack、Linear）を設定しておくと、クラウド上で自動実行される仕組みだ。

従来のClaude Codeは「ユーザーのマシンで動く」制約があった。ターミナルを閉じれば止まるし、ノートPCがスリープすれば中断する。Routinesはこの制約を取り払い、定期実行・API呼び出し・GitHubイベントをトリガーにした24時間稼働を可能にした。

夜間のPRレビュー、毎朝のバグスキャン、週次のコード品質チェックなど、「人間が寝ている間に進めておいてほしい」タスクに向いている。広告レポートの定期集計や、キャンペーンデータの夜間バッチ処理にも転用できる。

[Medium - The AI Studio](https://medium.com/the-ai-studio/anthropic-just-launched-claude-routines-6430dd721e4a)

---

## 楽天のAIチームが7時間の自律作業で99.9%精度を達成

楽天のAIチームが、大規模コードベースでactivation vector抽出を実装した事例が報告されている。Claude Codeに任せた結果、7時間のノンストップ自律作業で完了し、数値精度は99.9%を達成したという。

「7時間」というのがリアルだ。人間が横で見ていなくても、Claude Codeは勝手にコードを書き、テストを回し、失敗したら修正するサイクルを繰り返す。途中で止まったり、おかしな方向に暴走したりしなかったのは、タスクの仕様が明確だったからだろう。

逆に言えば、仕様が曖昧なタスクや、途中で人間の判断が必要なタスクには向かない。自律作業を成功させるには「何をもって完了とするか」を事前に定義しておく必要がある。

[Medium - TechTrends Digest](https://medium.com/techtrends-digest/claude-code-is-changing-how-we-build-software-in-2026-cba4a800297e)

---

## Telegramで遠隔操作 — qlaudeというアプローチ

「qlaude」は、Claude CodeをTelegram経由で制御するCLIラッパーだ。複数タスクをキューに積んでおき、Claude Codeが判断を求めてきたらTelegramで選択肢を選ぶ、という仕組み。

開発者の課題意識は「Claude Codeは便利だが、結局ターミナルの前に座っていないといけない」という点にあった。外出中やミーティング中でも、スマホからタスクの進捗を確認し、必要な判断だけ下せる。

タスクごとに使うモデル（Sonnet/Opus）を指定できる点も実用的だ。設定作業はSonnet、複雑な実装はOpusという使い分けで、コストを最適化できる。

[Medium - Agent Native](https://agentnativedev.medium.com/qlaude-queue-based-claude-code-automation-with-telegram-control-778de887f465)

---

## Skills活用で75%トークン削減 — 「Caveman」という発想

Jonathan Fulton氏が「Claude Code Skillsはチートコード」という記事を書いている。中でも面白いのが「Caveman」というスキルだ。

Cavemanの役割は「冗長な説明を削る」こと。Claude Codeは親切すぎて、毎回「〜を実行しました。これにより〜が改善されます」のような丁寧な説明を返してくる。Cavemanを有効にすると「Done. Token validation updated.」のような簡潔な応答に変わる。結果、トークン消費が75%削減される。

月額制のProプランなら気にならないが、API従量課金で大量のタスクを流すときには効いてくる。もうひとつ紹介されている「Codex Review」は、通常のコードレビューに加えて「敵対的レビュー」モードがあり、エッジケースや設計上の仮定を積極的に攻撃してくれる。人間3人分のレビュー以上の問題検出ができるという。

[Medium - Jonathan's Musings](https://medium.com/jonathans-musings/agent-skills-the-cheat-codes-for-claude-code-b8679f0c3c4d)

---

## OpenClawの設計思想をClaude Codeで再現する「ClaudeClaw」

Mark Craddock氏が、OpenClaw（オープンソースの自律エージェントフレームワーク）のアーキテクチャをClaude Code上で再現する方法を解説している。

OpenClawは「ゲートウェイ→スキルシステム→マルチチャネルインボックス→イベントバス」という4層構造を持つ。Claude Codeの最近のアップデート（ヘッドレスモード、フック、マルチエージェント編成）を組み合わせると、この構造の大部分を約500行のTypeScriptで実装できるという。

実用的なのは、Telegram、Discord、Slack、メールなど複数チャネルからのメッセージを単一エージェントで処理できる点だ。顧客からの問い合わせが複数チャネルに分散している場合、これを統合するハブとして機能させられる。

[Medium - Mark Craddock](https://medium.com/@mcraddock/building-claudeclaw-an-openclaw-style-autonomous-agent-system-on-claude-code-fe0d7814ac2e)

---

## GitHubで急増中 — Claude Codeワークフローのエコシステム

Claude Code本体は115,000スター、19,200フォークに到達した。周辺のワークフロー系リポジトリも活発で、「awesome-claude-code-workflows」「claude-code-spec-workflow」など、実務向けのレシピ集が増えている。

特に「spec-driven development」のパターンが人気だ。Requirements→Design→Tasks→Implementationという流れを定義しておき、Claude Codeに順番に実行させる。バグ修正用のショートカット（Report→Analyze→Fix→Verify）も用意されている。

エコシステムが成熟してきたことで、ゼロから設定を考える必要がなくなりつつある。まずは公開されているワークフローを試し、自社の業務に合わせてカスタマイズする、という導入パスが現実的になってきた。

[GitHub - awesome-claude-code-workflows](https://github.com/ithiria894/awesome-claude-code-workflows)
