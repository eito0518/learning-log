# git 開発の流れ

## 開発 から プルリクエスト

1. git checkout -b <新規 branch 名>
2. 新規 branch で開発を行う
3. git add . ステージングエリアに追加
4. git commit -m "コミットメッセージ"
5. git push origin main <新規 branch 名>
6. github で PR を作成し、マージ

## リモートリポジトリをローカルリポジトリに反映

1. git checkout main ブランチを移動
2. git fetch リモートの変更を取得
3. git merge origin/main リモートの変更をローカルに反映
4. git branch -d <使い終わった branch>
