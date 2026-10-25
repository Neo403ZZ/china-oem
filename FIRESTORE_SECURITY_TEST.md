# Firebase セキュリティ検証手順（SHOES-001）

状態：未合格（本番Firestoreに対する2アカウントの直接アクセス拒否テストは未実施）。Sparkプランで実施可能。

## ルールの検証
Firebase Console > Firestore Database > ルール > ルールシミュレーターで次を確認。
- users/userA/projects/projectA の読み取り：認証UID userA → 許可
- 同じドキュメントをUID userBで読み取り → 拒否
- 同じドキュメントを未ログインで読み取り → 拒否
- userAであっても update/delete → 拒否
- その他の親パスや無関係のコレクションの読み取り → 拒否

## 実際の2アカウントでの検証
1. テスト用GoogleアカウントAでダミー案件を保存。
2. ログアウトし、端末内の下書きと画面表示が消えることを確認。
3. アカウントBでログインし、Aの案件が一覧に表示されないことを確認。
4. Bの認証状態でAのFirestoreドキュメントを直接読み出すテストを行い permission-denied を確認。
5. Aの案件は消えていないことを確認。

シミュレーターの合格は本番接続テストの代わりではありません。ユーザーUID・個人情報・秘密鍵を公開GitHubに記載しない。公開中のFirestoreルールとGitHubの firestore.rules が一致することも確認する。