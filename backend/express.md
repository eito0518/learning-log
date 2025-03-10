# Express とは？

Express は Node.js で Web アプリケーションを構築するためのフレームワーク。

## ルーティングの分割

Express では、エンドポイントごとにルーティングを分けることでコードを整理できる。

const userRouter = require("./routes/users");　// ファイルの場所を指定
app.use("/api/users", userRouter); // 特定のパスを指定
このように、特定のパスに対して別のファイルでルートを管理する。

## Mongoose による API 設計

Mongoose を使って MongoDB とやり取りすることで、データの保存・取得・更新・削除 (CRUD) を行うことができる。

1. ユーザー管理 (users.js)

ユーザー情報の更新
• findByIdAndUpdate(req.params.id, { $set: req.body }) を使い、指定した userId の情報を更新。
• ユーザー自身 (req.body.userId === req.params.id) または管理者 (req.body.isAdmin) のみが更新可能。

ユーザー情報の削除
• findByIdAndDelete(req.params.id) を使い、指定した userId のユーザーを削除。

ユーザーの取得
• クエリパラメータを利用して userId または username でユーザー情報を取得。
• findById(userId) または findOne({ username }) を利用。

ユーザーのフォロー
• findById(req.params.id) でフォロー対象のユーザーを取得。
• followers に userId を $push してフォロワーを追加。
• followings に userId を $push してフォロー中のリストを更新。

ユーザーのフォロー解除
• followers から userId を $pull して削除。
• followings から userId も削除。

2. データの登録・管理

Mongoose を使うことで、任意のデータをデータベースに保存・管理できる。
一般的なデータ管理において、次の操作が必要になる。

データの作成
• クライアントから送信されたデータを new Model(req.body) で作成。
• .save() を実行し、MongoDB にデータを保存。

データの更新
• findById(req.params.id) でデータを取得。
• $set を使って更新するフィールドを指定し、updateOne() を実行。

データの削除
• findById(req.params.id) で対象のデータを取得し、deleteOne() で削除。

データの取得
• findById(req.params.id) で ID に基づいてデータを取得。
• find({条件}) を使って条件に合うデータを取得。

配列データの管理
• $push を使って配列型のデータを追加。
• $pull を使って特定のデータを配列から削除。

3. 関連データの取得

特定の条件に基づくデータの取得
• find({ userId: 条件 }) で関連データを取得。
• Promise.all() を使うことで、複数の関連データを並列に取得可能。

特定のユーザーに紐づくデータの取得
• クエリパラメータやリクエストボディを利用し、ユーザーの userId に関連するデータを検索。

学んだこと
• Express で API を設計する際、ルーティングを分割すると整理しやすくなる。
• Mongoose を使うことで、MongoDB のデータを簡単に操作できる。
• findById(), findOne(), updateOne(), deleteOne() などを活用して CRUD を実装できる。
• $push と $pull を使うことで、配列データ（いいねやフォロー）を効率的に管理できる。
• Promise.all() を使うことで、複数のデータを並列に取得できる。
