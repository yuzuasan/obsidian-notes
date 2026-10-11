2026/10/11

2026年10月時点で、AIコーディングサービスを選ぶなら、まず GitHub Copilot、Cursor、Claude Code、Gemini Code Assist、Windsurf あたりを押さえるのがおすすめです。

ただし、今回の比較では「人気があること」と「無料で実用的に使えること」を分けて考えます。人気の高いサービスでも、無料枠が少なかったり、複数ファイルの修正をAIに任せるとすぐに制限へ達したりするためです。

利用者数については、各社が同じ基準で世界の実利用者数を公表しているわけではありません。そこで、開発者向け調査での利用・検討率、知名度、開発環境への統合状況などを参考に整理します。

## 1. 有料・無料を含めた全体ランキング

2025年上期の開発者調査では、GitHub Copilotが53%、Cursorが49%、Claude Codeが29%、Gemini Code Assistが25%、Windsurfが17%でした。これは「利用中または今年利用を検討している」と回答した割合であり、世界全体の実利用者数ランキングではありません。

[image](https://www.google.com/s2/favicons?domain=https://artificialanalysis.ai\&sz=32)

Artificial Analysis



以下は利用者の多さ・知名度・実務での存在感を重視した、おおまかな比較です。厳密な利用者数順ではありません。

[GitHub 코파일럿 AI 코딩 라이선스 구독: Pro/Business 플랜 정품 보장](https://images.openai.com/static-rsc-4/eLjHBMbzNpunLWb5Zp2LEu5ihqSbRBmWja5idXhF7SSh_SPWWVWsrzshQDjB7I0BYfi_3hnAfY6DiOUCu6NQJUsACMKi7wgZjg7kg5RTXRv33uvf-UFmOYPhA-dqW9n0ebpDIyAWOj60dqcmGMigk2Zg2wFXSVAUowReGXDq4D4?purpose=inline)

### 1. GitHub Copilot

総合的な第一候補

VS Code、Visual Studio、JetBrainsなど、既存の開発環境に組み込みやすい定番サービス。コード補完、チャット、エージェントによる修正まで幅広く対応します。

無料プランあり。有料プランは月額10米ドルから。

[image](https://www.google.com/s2/favicons?domain=https://github.com\&sz=32)

GitHub



公式サイト：[GitHub Copilot](https://github.com/features/copilot)

[Cursor IA - El editor de código de IA](https://images.openai.com/static-rsc-4/vCFNiYiDhBvuHu02fyxPmgLjrXDcbrEwU1bGNN2oPl2cl9SvUUj0ouwlhxqJQvmIWrDEpirZEOsyAyK5gDq-pygG5ezmPlh4yfiCO_LCVgcZD-HJXtmxnp8qmstQMkwLj4LchqBZiznPYgVQ9HNN1K2P3P0DIiY5aZCyj1VPOeo?purpose=inline)

### 2. Cursor

AIとの対話を中心に開発したい人向け。コードベース全体を参照しながら、複数ファイルの編集やリファクタリングを進めるワークフローが特徴です。

無料プランあり。高度なAI機能を継続利用するなら有料プランを検討。

公式サイト：[Cursor](https://cursor.com/)

[Anthropic 逾 50 萬行原始碼外洩的警訊：拆解部署烏龍與 AI 時代的內部治理盲區](https://images.openai.com/static-rsc-4/KmRG0cWqPVcAHUfKyJkUSKqUubBVk3ifO98Kq1YqYQg2XfEpBX1jD1L1rMMKaF0o4wyNor_XdiiZ15qnWeakr-0r7TLh09vdjQgp0kZaSKxKrYCsuA_KopKOm4RUP0qv9ZD0-x7kIqrAEN_aa1sQ9Pz82YFgbFY0HkE6gp5K8fw?purpose=inline)

### 3. Claude Code

ターミナルからコードを調査・編集し、テストやコマンドの実行まで進めるエージェント型ツール。複雑な処理の理解や大規模な変更をAIに任せたい人に向いています。

基本的にClaudeの有料プランなどを通じて利用するサービス。無料だけで使い続ける用途には不向き。

公式サイト：[Claude Code](https://code.claude.com/)

[AI IDE List | AI IDEs, Coding Agents, and Developer Tools](https://images.openai.com/static-rsc-4/HZ-eoSSOa7rwdmK-Idy0li4-hTthrLNGv09QCf0xGZY8jZLNSihIBjbJVXoeeZruyWoARfCtKrsgyYfOU1L_Uu-a1QXPIn9WDp20-pG1zvbhLadvSjCNfBl0uWkRplJWASxvhvyQ-WNc7-SzExPJnng5OPfed2FXh2NnbBH2Tho?purpose=inline)

### 4. Gemini Code Assist

VS CodeやJetBrainsなどで使えるGoogleのコーディング支援サービス。無料で使える量を重視する人にとって、特に注目したい選択肢です。

個人向け無料プランあり。無料枠の実用性は後半で詳しく比較します。

公式サイト：[Gemini Code Assist](https://codeassist.google/)

[Windsurf Editor: IDE com IA para desenvolvimento ágil](https://images.openai.com/static-rsc-4/9LRfHZ9mSmmbiMk170bPYLhZ_UeFr6bjzTii8tlMU9H2pgKM7QG14pWsq83TfUhGYJC2-HqQv0qWYVx0pOPP0qHXUcaFex62S83D_PCmApwppMFIa-nJmqOZ4QBzbY5Uzn71JL48_69PswTyZorXSsjjPpzrSX_ttoes4LTqFyk?purpose=inline)

### 5. Windsurf

AIに作業の流れを任せながら開発するタイプのエディタ。コードの生成だけでなく、既存コードの理解や変更を対話形式で進めたい人向けです。

無料プランあり。利用量や高性能モデルの利用条件は契約前に確認したいサービスです。

公式サイト：[Windsurf](https://windsurf.com/)

[Amazon Q Developer · GitHub Marketplace · GitHub](https://images.openai.com/static-rsc-4/XBk2MTrOKgsZK1QINXHNgIml3T8Hy6OdiHt3O5sTLLnaj66kcV_PXiZmwcJXi0OQo0rTMu9HV8m36pnfCnGW2z670NvnRRsvEgUSdkEBYKoTu5ZKZF5XU0SkZ1HDluLD5a8L8JRgs6ImqKyf5CdheyRsQRaizWNkC-GOWi50gGw?purpose=inline)

### 6. Amazon Q Developer

AWSを使う開発者に特に有力。AWSのサービスや設定、クラウド関連コードの作成・調査を助けてくれます。

無料プランあり。AWS中心の開発なら、総合的な人気順位以上に有力な候補です。

公式サイト：[Amazon Q Developer](https://aws.amazon.com/q/developer/)

このほか、ブラウザ上でアプリを作る Replit、画面やWebアプリの生成に強い Bolt.new、Lovable、UIの生成に強い v0 も人気のある選択肢です。これらは、VS Codeで普段のプログラミングを補助するツールとは用途が少し異なります。

[image](https://www.google.com/s2/favicons?domain=https://artificialanalysis.ai\&sz=32)

Artificial Analysis



## 2. 無料プラン限定ランキング

こちらは評価基準を変えます。重視するのは次の4点です。

- 利用量： 毎月どのくらいAIにコードを書かせられるか
- 制限の明確さ： 上限が公開されていて、残量を把握しやすいか
- 実用性： コード補完だけでなく、質問・バグ修正・複数ファイルの変更にも使えるか
- 継続性： お試しで終わらず、翌月以降も無料で使えるか

なお、Googleの個人向け Gemini Code Assist については、2026年6月のサービス変更があるため、以前の無料枠の情報をそのまま現在の評価に使うことはできません。

[image](https://www.google.com/s2/favicons?domain=https://developers.googleblog.com\&sz=32)

Google Developers Blog



### 無料枠の実用性ランキング

無料で個人利用する場合のおすすめ順。公式に公開されている利用上限と機能をもとに評価しています。無料枠は変更されるため、利用量が明示されていないサービスは推測で補っていません。

[Google Antigravity 使い方完全ガイド：インストールからGravity Modeまで【2026年版】 | ぽんずテックブログ](https://images.openai.com/static-rsc-4/EARmnfLcOdzii5KllIBAb2rDaLsyz00-6YNASrOy6xoJs55a9W_f3UP8L2vLvpgqCUjDb9e8bYvKzwFCjvIwk_dvNJA17U8iJONhcj1z2AIoK7Nu9ipr8Yih8ZgB5ICauRJd2o2lJnOVVnlSbnOgO1WBUhKzr-VRbzr1YA9eSAI?purpose=inline)

### 1. Google Antigravity

まず無料で試したい人向け

Googleの新しいエージェント型開発環境。以前のGemini Code Assistの無料枠と混同しないことが重要です。2026年6月にGemini CLIなどの提供体制に変更があり、Antigravityが新しい選択肢になっています。

評価：有力候補。ただし、今回確認できた公式情報だけでは現在の無料利用量を確定できないため、無料枠の量については保留。

公式情報：[Google Developers Blog](https://developers.googleblog.com/an-important-update-transitioning-gemini-cli-to-antigravity-cli/)

[Jual Github Copilot 12 Months Private | Shopee Indonesia](https://images.openai.com/static-rsc-4/yiRC1zIxJnt3bg3KS5QBJdb-bQnGsC8ovHkaHsMSj9MtIvxLzUyHVBOKuehXqoNdvbO6sesOQ8oFITkMlQ2hQ3dR18JwnvUsgDE0ZilZkcTtTVXtKYKcsdEi925sXAuOaeNUDEW_AqU5F0RDTgXDtT5-E2Kfl-4MB02F3ysOgK4?purpose=inline)

### 2. GitHub Copilot Free

無料枠が明確

VS Codeなどで使い始めやすく、コード補完とチャットを両方試せます。学習用や小規模なプログラムには十分便利です。

公式に確認できる目安：月2,000回のコード補完。チャットやエージェント機能には別途利用制限があります。

[image](https://www.google.com/s2/favicons?domain=https://github.com\&sz=32)

GitHub

+1



公式サイト：[無料で始める](https://github.com/features/copilot)

[Cursor - AI Code Editor Tool for Faster Development & Developers | itirupati.com](https://images.openai.com/static-rsc-4/VpUBKVJVXV7fNb9cW9lC0WwEL7Ev1STMOU_rUGs7nYGJI1GxggS-Un3YnjzA5gGYQhB5TsMPr_szy4uKNTPoR996TcSkTRzp6q98AszBFPpQTz4JehMRk9sFuSdUZGXAliKMx7PidH8Qz62gY_LIw3fa7y4qecELtwYCHI2tAJw?purpose=inline)

### 3. Cursor Hobby

AIエディタの操作感を試したい場合におすすめ。Agentによるコード変更や補完を体験できます。

無料枠：Agentリクエストや補完に制限あり。公式料金ページで固定の上限数を確認できないため、Copilotのように月間回数で単純比較できません。

[image](https://www.google.com/s2/favicons?domain=https://cursor.com\&sz=32)

料金プラン

+1



公式サイト：[料金・無料枠](https://cursor.com/ja/pricing)

[Amazon Q Developer CLIに画像からCloudFormationテンプレートを生成させる – TechHarmony](https://images.openai.com/static-rsc-4/VBX8Ryz2KU5IIUMl0YCBYpZ8L56vAu4wFMbJpgwdQUTOnsUpK8Q4SPFkq4shXdxH_wa_wfcrklyG13flEVjJwWGpVW13AX4brV1OlvdmjXy4dGxvPFGiTVPCOXIq1gOZ13wyBKHC6Fx2zn5AhoO9CQabqjyx-1dBSpjHk8xQNGM?purpose=inline)

### 4. Amazon Q Developer Free

IDE内のコード補完や質問に対応し、AWS関連の開発に特に向いています。Javaのコード変換機能もあります。

公式の無料枠：月50回のエージェントリクエスト。Javaコード変換は月1,000行まで。

[image](https://www.google.com/s2/favicons?domain=https://aws.amazon.com\&sz=32)

AWS

+1



公式サイト：[料金・無料枠](https://aws.amazon.com/jp/q/developer/pricing/)

## 無料枠を数字で比較

| サービス               | 無料で使える量・制限                         | 無料での実用性       |
| ------------------ | ---------------------------------- | ------------- |
| GitHub Copilot     | 月2,000回のコード補完。チャット等にも制限            | 学習・日常的な補完に向く  |
| Cursor Hobby       | Agent・補完ともに制限あり。上限数は公式ページで明示されていない | AIエディタの体験向き   |
| Amazon Q Developer | 月50回のエージェントリクエスト                   | AWS・Java開発に向く |
| Google Antigravity | 現行の無料枠の具体的な上限は未確認                  | 最新の条件確認が必要    |
| Claude Code        | 無料だけで継続利用する選択肢としては不向き              | 有料プランを検討      |

[image](https://www.google.com/s2/favicons?domain=https://github.com\&sz=32)

GitHub

+3

※「コード補完1回」と「AIへの質問1回」は同じではありません。また、エージェントが複数ファイルを読んで修正する作業は、単純なコード補完より多くの利用枠を消費する場合があります。

## 3. 結局、どれを選ぶのがよい？

プログラミング学習を無料で続けたい

GitHub Copilot Freeから始めるのがおすすめ。コードの意味を質問したり、短いメソッドを書いてもらったりする使い方に向いています。

AIに複数ファイルを編集させたい

Cursor Hobbyを試すのがよいでしょう。ただし、無料枠が限られているため、毎日長時間使う用途では制約を感じる可能性があります。

AWSやJavaの開発をしている

Amazon Q Developerが候補です。AWSとの関連が深いプロジェクトでは、一般的な人気順位以上に役立つことがあります。

将来的に有料契約も考えている

まずGitHub Copilot FreeとCursor Hobbyを同じ小さなプロジェクトで試し、コードの正確さ、修正のしやすさ、無料枠の減り方を比べるのが合理的です。

私の結論： 利用者の多さと導入しやすさならGitHub Copilot、AI中心の開発体験ならCursor、AWS開発ならAmazon Q Developerを優先候補にします。無料枠の「量」だけで決めず、実際にどの作業まで無料で完了できるかを比べるのがポイントです。