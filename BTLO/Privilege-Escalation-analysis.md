# Linux Privilege Escalation - Analysis Notes

## Observation
- Web directory 上でファイル操作の痕跡を確認
- 特定ユーザーのホームディレクトリを探索
- 権限の高い実行ファイルを検索している挙動

## Hypothesis
- 攻撃者は初期アクセス後、権限昇格を試みている可能性。

## Interesting Behavior
- Python を利用したシェルの安定化を確認。
- 権限付きバイナリの探索が継続して行われていた。

## Insight
- Privilege Escalation は exploit 実行以前に
  「環境調査フェーズ」が長いことを再認識。
