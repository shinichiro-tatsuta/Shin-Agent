---
title: "Claude Code 今日の発見 — 2026-04-06"
emoji: "🔍"
type: "idea"
topics: ["claudecode", "ai", "automation"]
published: true
---

# Claude Code 今日の発見 — 2026-04-06

コードを書くだけじゃない。Claude Codeは「業務の摩擦」を消すツールとして、予想外の領域に浸透し始めている。

---

## Polymarketの自動売買システムを会話だけで構築した男

予測市場Polymarketで、価格監視からアービトラージ検出、売買執行までを完全自動化したシステムがClaude Codeとの「1回の会話」で生まれた。開発者のÖrvar Karlssonが採用したのは、PolymarketのRust製CLIをPythonでラップし、それをClaude Codeに操作させるというアプローチだ。

特に秀逸なのはNegRiskスキャナーと呼ばれるモジュール。複数の選択肢があるマーケットで、全選択肢のYES価格を合計すると本来1ドルになるはずが、0.70ドルしかないケースを検出する。これは理論上確実に利益が出る裁定機会で、実際に36.2%のリターンを叩き出したという。

当初はFastAPI + Next.jsのダッシュボードも作ったが、「結局ターミナルで全部できる」と気づいて破棄。最終的に8トレードで勝率75%、ROI +9.6%を記録した。金融システムの自動化というと大げさに聞こえるが、「CLIを叩けるなら何でも自動化できる」という発想は応用範囲が広い。

[Medium](https://medium.com/@rvarkarlsson/building-an-automated-polymarket-trading-system-with-claude-code-1982ff60cc74)

---

## 経済学PhDコースで10種類のAIエージェントが論文をレビューする

Emory大学のPedro Sant'Anna教授が、博士課程「Econ 730: Causal Panel Data」の講義資料を作るために構築したワークフローが異様に本格的だ。800枚以上のスライド、Quarto版のインタラクティブ資料、Rの再現パッケージ——これらすべてを管理するために、10種類の専門エージェントが並列で動く。

Proofreaderが言語をチェックし、Slide-auditorがレイアウトを検査し、Pedagogy-reviewerが「教え方として効果的か」を13のパターンで評価する。さらにCriticエージェントが厳しく指摘し、Fixerエージェントが修正する——この敵対的なループを最大5回繰り返して品質を担保する。コミット可能な閾値は80点、PR作成は90点、95点で「優秀」という明確なゲートも設けている。

2026年3月時点で、シカゴ大学、ベイラー大学など15以上の研究グループがこのテンプレートをフォークして使っている。論文執筆や資料作成の品質管理プロセスとして、広告制作物のレビューフローにも転用できそうな構造だ。

[GitHub](https://github.com/pedrohcgs/claude-code-my-workflow)

---

## 前提知識ゼロでiOSプロジェクトに途中参加、無事リリースした話

TVerのiOSエンジニア・福島氏は、大規模プロジェクトの「不具合解消フェーズ」から途中参画することになった。プロジェクト固有の要件も実装アプローチもほぼ把握していない状態。そこで3つのClaude Codeスキルをワークフロー化した。

`/analyze-and-create-issues`で不具合を分析しIssueを自動生成、`/implement-issue`でそのIssueを参照しながら実装、`/create-pr`でAndroid実装との比較表を含むPRを作成——この3ステップを回すことで、キャッチアップと実装を同時に進められた。

記事のポイントは「バグ修正はAI活用と相性が良い」という指摘。ゴールが明確で、スコープが限定的で、調査プロセスを自動化しやすい。新規開発よりも、既存コードの修正や改善タスクにClaude Codeを投入するほうが効果的という示唆は、クライアントワークでも参考になる。

[TVer Tech Blog](https://techblog.tver.co.jp/entry/claude-code-use)

---

## 広告分析が3〜5時間から「体感7分」に

RimoでRevOpsとマーケティングを担当する佐伯氏は、PowerShellで4画面分割してClaude Codeを並列実行している。最も効果が出ているのは広告分析だ。

従来は管理画面を確認し、キーワードを精査し、改善案を作成するのに3〜5時間かかっていた。今はBigQueryに格納した広告データから数字を自動抽出し、状況要約・考察・改善提案を生成するスキルを自作して回している。所要時間は「体感7分くらい」。

興味深いのは「提案はAIに出してもらい、採用するかどうかは人が決める」という運用方針。完全自動化ではなく、人間の判断を残すことで、AIの暴走リスクを抑えつつ効率化の恩恵を受けている。広告運用チームがClaude Codeを導入するときの現実的なモデルケースだ。

[Rimo](https://rimo.app/@rimo/general/claude_code_ad_reporting)

---

## 500商品のタグ付けが「数分」で終わる世界

ECサイト運営者向けの記事によると、500点の新商品を登録する作業——商品説明の作成、メタデータの付与——は従来「数日」かかっていた。これがClaude Codeを使うと「数分」で終わるという。

具体的には、WooCommerceのデータをClaude 3.7 APIに流し込み、SEO最適化された商品説明を自動生成、バックエンドにメタデータを同期させる。週に15〜25時間の手作業が消える計算だ。

商品マスタ整備や在庫データのクレンジングなど、「やればできるけど面倒」な作業は広告・マーケ領域にも多い。データ入力系の定型業務は、Claude Codeの最も即効性が高い適用領域かもしれない。

[Stormy AI Blog](https://stormy.ai/blog/agentic-commerce-claude-code-automation-2026)

---

## browser-useが8万スター、「フォーム入力は全部お任せ」の時代

Claude Codeと組み合わせるブラウザ自動化ツールとして、browser-useが注目を集めている。GitHubで8万スター超のPythonフレームワークで、MITライセンス。

他のツールと違うのは「自律エージェントモード」の存在だ。「この求人に応募して」と指示すれば、フォームのフィールドを識別し、適切な値を選択し、テキストを入力する——ステップバイステップの指示なしで、マルチページのワークフローを自動で完遂する。

記事の筆者は「採用プラットフォーム（Greenhouse、Ashby）への応募作業」「デプロイ後のスクリーンショット確認」「認証のCookie維持」などで活用。ただし「全部これ1つ」ではなく、SNS閲覧には軽量なPinchTab（800トークン）、自律ワークフローにはbrowser-useと使い分けているのがリアルだ。

[DEV Community](https://dev.to/minatoplanb/i-tested-every-browser-automation-tool-for-claude-code-heres-my-final-verdict-3hb7)

---

## Claude CodeのPython再実装が一晩で10万スター

4月上旬、Claude Codeのソースコード（51.2万行）が意外な形で公開され、中国の開発者Sigrid Jinが「彼女のアドバイス」を受けて動いた。やったことは、OpenAI Codex（oh-my-codex）を使い、一晩でPythonによる再実装を完成させること。

「2人、10個のOpenClawアカウント、MacBook Pro 1台」で、オリジナルのコードを1行も使わずにアーキテクチャだけを再現した。結果、AnthropicからのDMCA申請をかわしつつ、「史上最速で10万スターを獲得したGitHubプロジェクト」という珍記録が生まれた。

技術的な再現性より、「AIでAIツールを再実装する」というメタな構図が面白い。Claude Codeの内部構造を理解したい開発者にとっては、このPython版が格好の教材になっている。

[量子位](https://www.qbitai.com/2026/04/394570.html)
