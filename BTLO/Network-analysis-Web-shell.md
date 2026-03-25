# Incident Analysis: Web Shell Upload & Reverse Shell Connection
Category: Network Analysis / Incident Response
Platform: Blue Team Labs Online (BTLO)
Analyzed by: Sakata Kyousuke

## 1. Executive Summary
内部ネットワーク内の特定IPによるポートスキャンを起点とした、Webシェルアップロードおよびリバースシェル接続のインシデントを特定しました。パケット解析により、攻撃者が偵察ツールを用いてWebサーバーの脆弱性を特定し、悪意のあるPHPファイルを実行することで制御権を奪取したプロセスを確認。本件はTrue Positiveと断定し、即時隔離およびフォレンジック調査が必要です。

---

## 2. Technical Analysis (Pcap Investigation)
### Phase 1: Reconnaissance (偵察)
Activity: 内部IPによる広範囲なポートスキャン。

Method: TCP SYN Scan (Port: 1-1024)。

Identified Tools: HTTPリクエストの User-Agent より、以下の偵察ツールの使用を確認。

[Tool Name 1]

[Tool Name 2]

### Phase 2: Exploitation (脆弱性悪用)
Vector: Webサーバーへのファイルアップロード機能の悪用。

Observation: パケットシーケンスより、特定のPHPファイルへの不審なPOSTリクエストを特定。この際、/uploads ディレクトリへ悪意のあるファイルが書き込まれた痕跡を確認。

### Phase 3: Delivery & Installation (Webシェル設置)
Malicious File: /uploads/[Filename].php

Evidence: 当該ファイルへのアクセス直後に ?cmd= パラメータを伴うリクエストを確認。これによりリモートでのコマンド実行が可能なWebシェルとして機能していることを断定。

### Phase 4: Command & Control (リバースシェルの確立)
Activity: Webシェルを起点としたリバースシェルの実行。

Connection: 攻撃者の制御端末とターゲットサーバー間で、特定ポート（Port: [Number]）を介した双方向通信の成立を確認。

---

## 3. Risk Assessment & Mapping
### Verdict: True Positive (Critical)

MITRE ATT&CK Mapping:

Reconnaissance: T1595 (Active Scanning)

Persistence: T1505.003 (Server Software Component: Web Shell)

Command and Control: T1090 (Proxy) / T1059 (Command and Scripting Interpreter)

---

## 4. Proposed Response (SOC Recommendations)
Isolation (隔離):

侵害されたサーバー（Destination IP）および攻撃元（Source IP）のネットワーク隔離。

Eradication (除去):

アップロードされた悪意のあるPHPファイルの削除。

リバースシェルに使用されたプロセスの強制終了。

Vulnerability Management:

Webアプリケーションのファイルアップロード機能におけるバリデーション不備の修正。

Forensics:

サーバーログの精査による、Webシェル実行後の特権昇格（Privilege Escalation）や横展開（Lateral Movement）の有無の確認。
