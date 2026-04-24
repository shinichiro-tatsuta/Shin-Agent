---
title: "Claude Code 今日の発見 — 2026-04-24"
emoji: "🔍"
type: "idea"
topics: ["claudecode", "ai", "automation"]
published: true
---

# Claude Code 今日の発見 — 2026-04-24

「自律と協調」がキーワードだった一日。単独のAIが賢くなるだけでなく、複数のエージェントがチームとして動き、人間の関与を「指示と確認」に絞り込む事例が目立った。

---

## 16台のClaudeがCコンパイラを1ヶ月で書き上げた

Anthropicの研究員Nicholas Carliniが、16個のClaude Codeインスタンスを並行稼働させ、Linuxカーネルをビルドできる本格的なCコンパイラを約1ヶ月で構築した。コード量は10万行のRust。最終的にLinux 6.9カーネルの起動に成功し、x86・ARM・RISC-Vに対応している。APIコストは約2万ドル。

各エージェントは独立したDockerコンテナで動き、Gitリポジトリを通じて間接的に協調する。タスクの競合はGitプッシュの成否で自動調整される仕組みだ。これは「コンパイラを作る」プロジェクトというより、「複数のAIエージェントを長期間協働させる工学的手法」の実験であり、その意味で成功している。広告クリエイティブの大量生成やキャンペーン検証の並列化にも同じアーキテクチャが使えそうだ。

[IceYao's Blog](https://www.iceyao.com.cn/2026/04/15/claude-parallel-agents-c-compiler/)

---

## Claude Codeを「Level 5」まで育てると、開発は指示と確認だけになる

Qiitaに投稿された記事が、Claude Codeの習熟を5段階で整理している。Level 1は素のプロンプト、Level 2でCLAUDE.md（プロジェクトルールを記述したファイル）を導入、Level 3で手順書をSkillsに分離、Level 4でHooksによる自動テスト・整形、Level 5で複数のレビュワーエージェントを並行稼働させる。

Level 5に到達すると、人間の作業は「何を作るか決める」と「動くか確認する」だけになる。著者は「繰り返しの苦痛が次のレベルへの動機になる」と書いており、段階的に仕組みを積み上げていく現実的なアプローチだ。クライアントワークで毎回同じ説明をしている作業があれば、まずSkillsに切り出すところから始められる。

[Qiita](https://qiita.com/teppei19980914/items/8da88b33ffa8cf88dfa2)

---

## エムスリーのQAエンジニア、テスト時間を74%削減

医療系IT企業エムスリーのQAエンジニアが、Claude Codeを活用してE2Eテストの実行時間を105分から27分に短縮した。年間68時間分のCI/CD待機時間が消えた計算になる。

技術的には3つのアプローチが効いている。まず、固定3秒の待機処理をAPIレスポンス完了まで待つ動的待機に変更。次にPage Objectパターンでセレクターをビジネスロジックから分離。最後に、SaaS型ツールの同時実行数制限から解放され、Playwrightのworker数を自由に設定できるようになった。さらにMCP（Model Context Protocol）を使って「テスト実行→Confluence更新→JIRAチケット作成」の流れも自動化している。6ヶ月で67件のPR/MRをマージしたというのも印象的だ。

[エムスリーテックブログ](https://www.m3tech.blog/entry/2026/04/20/090035)

---

## qlaude：Telegramでタスクを投げて、Claudeがキューで処理する

qlaudeはClaude CodeのCLIラッパーで、複数タスクをキューで順番に処理し、対話的な判断が必要なときにTelegramで通知を受けられる。「Sonnetでプロジェクト設定→Opusでビジネスロジック実装→Sonnetでテスト作成」といった具合に、タスクごとにモデルを指定することも可能だ。

開発者が解決したかったのは、Claude Codeの「一発セッションと継続的スループットの間のギャップ」だという。寝る前にタスクを積んでおいて、朝起きたら結果を確認する、といった運用ができる。代理店のルーティンワーク、たとえばレポート生成や入稿データのチェックを夜間バッチで流す使い方が思い浮かぶ。

[Medium](https://agentnativedev.medium.com/qlaude-queue-based-claude-code-automation-with-telegram-control-778de887f465)

---

## Anthropicの3分離パターン：計画・生成・評価を別エージェントに

Anthropicが推奨する「Plan-Generate-Evaluate」パターンをClaude Codeのサブエージェントで実装した事例がQiitaに出ている。単一エージェントに長時間タスクを任せると品質が下がるため、計画を立てるPlanner、コードを書くGenerator、結果を検証するEvaluatorを分離する。

面白いのは、Anthropicの経験として「生成者に自己批判させると、自分の成果物を過大評価しがち」という問題が報告されている点だ。独立した評価エージェントを厳しくチューニングするほうが実効的だと結論づけている。このパターンでメインスレッドのトークン消費が4〜5分の1に減ったという報告もある。クリエイティブ制作で企画・制作・品質チェックを分けるワークフローと相性がよさそうだ。

[Qiita](https://qiita.com/nogataka/items/efe8eb9df612d2211221)

---

## Claude Managed Agents：顧客オンボーディングが3〜5営業日から2時間に

4月8日にパブリックベータが始まったClaude Managed Agentsの企業ユースケースがまとめられている。たとえば顧客オンボーディングでは、従来3〜5営業日・15〜20の人的タッチポイントが必要だったプロセスが2時間以下に短縮された。KYC認証からアカウント設定、システム統合まで自動で処理される。

法務チームでは契約書処理が1件45分から3分に。セキュリティ監査では夜間に自動スキャンを走らせ、異常パターンを学習ベースラインと比較して優先度付けした結果を朝に報告。誤検知が70〜80%減ったという。複数ステップ・長時間実行・複数システム連携が必要なケースがManaged Agentsの適用領域だ。

[BSWEN](https://docs.bswen.com/blog/2026-04-09-claude-managed-agents-use-cases/)

---

## ClaudeClaw：OpenClawのアーキテクチャをClaude Codeで再現

OpenClawはオーストリアの開発者Peter Steinbergerが作ったオープンソースの汎用AIエージェントフレームワークで、2025年11月のリリース後にGitHub史上最速で成長したリポジトリとして知られる。WhatsAppやTelegramなどのメッセージングアプリに接続し、メール管理やカレンダー自動化、ウェブスクレイピングなどを自律的に行う。

その設計思想をClaude Codeで再現した「ClaudeClaw」の実装記事がMediumに出ている。Gateway・Skills・マルチチャネルインボックス・イベントバスの4層構造を、Claude Codeのheadlessモードとhooksで模倣する。v2.1.80で追加されたTelegram/Discordのネイティブチャネル対応により、カスタムアダプター不要で複数プラットフォームを扱えるようになった。

[Medium](https://medium.com/@mcraddock/building-claudeclaw-an-openclaw-style-autonomous-agent-system-on-claude-code-fe0d7814ac2e)
