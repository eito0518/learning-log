# Express とは？

Express は Node.js で Web アプリケーションを構築するためのフレームワーク。

## ルーティングの分割

Express では、エンドポイントごとにルーティングを分けることでコードを整理できる。

```js
// server.js
const userRouter = require("./routes/users"); // ファイルの場所を指定
app.use("/api/users", userRouter); // 特定のパスを指定

// some_route.js
const router = require("express").Router();
```

## Mongoose による API 設計

Mongoose を使って MongoDB とやり取りすることで、データの保存・取得・更新・削除 (CRUD) を行うことができる。

### データの保存・取得・更新・削除 (CRUD)

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
