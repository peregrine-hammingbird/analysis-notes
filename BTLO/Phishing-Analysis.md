# Incident Analysis: Phishing Email Investigation (BTLO)

## 1. Executive Summary
本レポートは、Blue Team Labs Online (BTLO) におけるフィッシングメール解析チャレンジの結果をまとめたものである。不審な `.eml` ファイルの解析を通じて、攻撃者のインフラ（IP/Host）および誘導先のフィッシングサイトを特定。解析結果に基づき、SOCアナリストの視点から「Patient Zero（最初の感染者）」の特定と被害拡大防止のための推奨アクションを策定した。

---

## 2. Technical Investigation

### Phase 1: Email Header Forensics
メールヘッダーを解析し、攻撃の起点となる送信元情報を特定。
*   **Tool Used:** MousePad, Thunderbird, Whois (DomainTools)
*   **Key Artifacts:**
    *   **Subject:** [Challengeでの件名を入力]
    *   **Source IP:** [特定したIPを入力]
    *   **Reverse DNS:** 送信元IPの逆DNS解決を実施し、攻撃者が利用したホスト名を確認。

### Phase 2: Artifact & URL Analysis
メール本文および添付ファイルに含まれる悪意のある要素を調査。
*   **Attachment:** 添付ファイル名の確認およびハッシュ値（MD5/SHA256）の意識。
*   **Malicious URL:** 本文中のリンクを抽出。
*   **Hosting Provider:** URLがホストされているプラットフォーム（AWS, Azure, Firebase等）を特定。
*   **Visual Evidence:** `URL2PNG` を使用し、安全な環境下でフィッシングサイトのヘッダーテキストおよび外観をキャプチャ・分析。

---

## 3. Incident Response Strategy (SOC Perspective)

分析結果に基づき、実務において推奨される初動対応（SOP）を以下に定義する。

### 🚨 Phase 1: Containment (封じ込め)
1.  **Scope Identification:** 同一ドメインからのメールを受信した全ユーザーをSIEM/メールゲートウェイで検索。
2.  **Host Isolation:** 添付ファイルを実行、またはURL先で情報を入力した疑いのある端末をネットワークから即時隔離。
3.  **Credential Management:** 情報入力の疑いがある場合、当該ユーザーのAD/SaaSアカウントのセッションを強制終了し、パスワードをリセット。

### 🔍 Phase 2: Investigation (調査)
*   **Lateral Movement Check:** 隔離端末のEDRログを確認し、不審なプロセス生成（`cmd.exe`, `powershell.exe`）や内部スキャンの痕跡を調査。
*   **Malware Analysis:** 添付ファイルがダウンロードされた場合、サンドボックス環境で動的解析を行い、C2通信先を特定。

### 🛠️ Phase 3: Eradication (根絶)
*   メールサーバーから該当メールを一括削除。
*   プロキシおよびファイアウォールにて、特定した悪意のあるURL/IPをブラックリストに登録。

---

## 4. Lessons Learned & Prevention
*   **Technical Control:** SPF/DKIM/DMARCの不備確認、およびURLサンドボックス製品の導入検討。
*   **Security Awareness:** 定期的なフィッシング訓練の実施と、不審メール受信時の報告フロー（SOCへのエスカレーション）の周知徹底。

---
**Author:** Sakata Kyousuke (坂田 杏介)  
**Date:** March 2026  
**Tools:** MousePad, Thunderbird, URL2PNG, Whois.DomainTools
