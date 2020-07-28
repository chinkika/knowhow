

#### 作業時のメモ ####


##### 1.よく使うgitコマンド
```
git clone  -b ブランチ名　https://github.com/ユーザー名/リポジトリ名.git
→新しいブランチをローカルに持ってくる

git status
→変更点を表示

git add .
→修正ファイルを追加

git commit -am ‘message’
→修正ファイルをメッセージ付でコミット

git push origin master
→masterブランチにpush

git pull origin feature_branch
→サーバー上のfeature_branchの更新をローカルのブランチにマージ

git checkout -b <branch name> origin/<branch name>
→特定なブランチをチェックアウトしたい

git stash
→修正を一時退避

git stash list
// こんな感じで出力されます
stash@{0}: WIP on test: xxxx
stash@{1}: WIP on commit-sample: xxxx

git stash apply stash@{0}
→一時退避したstash@{0}の作業をもとに戻します

git fetch --prune origin
→sourcetreeフェッチでもサーバー上既に消えたブランチは更新されず
```
