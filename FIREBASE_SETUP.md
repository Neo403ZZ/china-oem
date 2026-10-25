# MY BRAND OEM クラウド機能の初期設定

未設定の状態ではマイページのボタンは無効です。GitHub PagesだけではGoogleログイン・サーバー保管は実現できません。

1. https://console.firebase.google.com/ でFirebaseプロジェクトを作成し、Webアプリを登録する。
2. Authentication > Sign-in method でGoogleを有効にする。Authentication > Settings > Authorized domains に `neo403zz.github.io` を追加する。
3. Firestore Databaseを作成する。Firestore Rulesへ `firestore.rules` の内容をコピーして **公開** する。テストモードのまま放置しない。
4. プロジェクト設定 > アプリ > SDKセットアップ > 構成を表示し、Webアプリ設定の公開値だけを `firebase-config.js` の `null` と差し替えて記載する。例：`window.MYBRAND_FIREBASE_CONFIG = {apiKey:"...",authDomain:"...",projectId:"...",appId:"..."};`。サービスアカウント鍵・管理者秘密鍵は記載しない。
5. GitHub Pages公開後、`mypage.html` でGoogleログイン→新規案件保存→再読み込み→表示確認→ログアウト→他アカウントからの参照不可を確認する。

注意：現在の案件保存は名称・カテゴリ・状態・作成日時だけです。靴仕様や画像ファイル、ファイルアップロードは未実装です。Googleログイン・Firestoreを使用するにはFirebaseプロジェクトの管理権限と利用規約・プライバシーポリシー等の準備が必要です。公開の際にはGoogleのOAuth同意画面や個人情報の取り扱いも確認してください。

## v0.2 靴の下書き連携
靴ページの端末内下書き（テキスト・サイズ数量）を新規案件と一緒に保存し、マイページの「靴の下書きを復元」から端末内へ復元します。復元時には上書き確認が表示されます。画像ファイルは保存対象外です。

Firestoreルールを最新版へ更新しない限り、v0.2の案件保存は拒否されます。Firebaseの設定後に、保存・再読み込み・別端末復元・他アカウントの読取拒否を実機でテストしてください。
