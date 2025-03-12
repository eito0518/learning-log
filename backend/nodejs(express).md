# Node.js とは？

## npm とは？

Node.js のパッケージマネージャー。`package.json` で管理できる。

## よく使う npm コマンド

- `npm init -y` → `package.json` を作る
- `npm install <package>` → パッケージをインストール
- `npm uninstall <package>` → パッケージを削除

# Express とは？

Express は Node.js で Web アプリケーションを構築するためのフレームワーク。

## ルーティングについて

Express では、エンドポイントごとにルーティングを分けることでコードを整理できる。

```js
// server.js
const userRouter = require("./routes/users"); // ファイルの場所を指定
app.use("/api/users", userRouter); // 特定のパスを指定

// some_route.js
const router = require("express").Router();
```

## npm Mongoose 　について

Mongoose を使って MongoDB とやり取りすることで、データの保存・取得・更新・削除 (CRUD) を行うことができる。

### Mongoose 接続

### データの保存・取得・更新・削除 (CRUD) API 設計

クライアントから送信されたデータを保存

```js
router.post("/", async (req, res) => {
  // モデルのインスタンスを作成
  const newData = new Model(req.body);
  // データベースに保存
  const savedData = await newData.save();
  res.status(200).json(savedData);
});
```

データの取得

```js
router.get("/:id", async (req, res) => {
  // _id に基づいてデータを取得
  const data = await Model.findById(req.params.id);
  res.status(200).json(data);
});

router.get("/", async (req, res) => {
  // 条件に基づくデータを1つ取得
  const filteredData = await Model.findOne({ category: req.body.value });
  res.status(200).json(filteredData);

  // 条件に基づくデータを全て取得
  const filteredData = await Model.find({ category: req.body.value });
  res.status(200).json(filteredData);
});
```

データの更新

```js
router.put("/:id", async (req, res) => {
  // _id に基づいてオブジェクトデータを更新
  const updatedData = await Model.findByIdAndUpdate(
    req.params.id, // _id で検索
    { $set: req.body }, // 更新する情報
    { new: true } // 更新後のデータを返す
  );
  res.status(200).json(updatedData);
});
```

データの削除

```js
// _id に基づいてデータを削除
router.delete("/:id", async (req, res) => {
  await Model.findByIdAndDelete(req.params.id);
  res.status(200).json("データを削除しました");
});
```

## npm MySQL2

https://qiita.com/miyabisun/items/3a139f8f48aa34f6d566?utm_source=chatgpt.com

###　 MySQL2 　接続

### データの保存・取得・更新・削除 (CRUD) API 設計
