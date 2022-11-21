# 何の練習？
1. branchAからbranchBを作成
2. branchA -> mainのPR作成
3. branchB -> branchAのPR作成
4. branchAを更新してpush

のような操作をした時、branchB -> branchAのPRにてFiles changedが更新されずbranchB作成時点のbranchAとの変更点が表示される。
原因は[ここ](https://docs.github.com/ja/pull-requests/collaborating-with-pull-requests/proposing-changes-to-your-work-with-pull-requests/about-comparing-branches-in-pull-requests#three-dot-and-two-dot-git-diff-comparisons)に書いてある通り。
branchA更新後と比較したい場合は、branchBで`git merge origin/branchA`のようにすればできる。


# 練習に使ったコマンド
`history`で出力

```
echo "branchA-1" > branchA.txt
git add branchA.txt
git commit -m "branchA-1"
git push origin branchA
（branchA -> mainのPR作成）
git checkout -b branchB
echo "branchB" > branchB.txt
git add branchB.txt
git commit -m "branchB"
git push origin branchB
（branchB -> branchAのPR作成）
git checkout branchA
echo "branchA-2" >> branchA.txt
git add branchA.txt
git commit -m "branchA-2"
git push origin branchA
（branchB -> branchAのPRのFiles changedが更新されていないことを確認）
git checkout branchB
git merge origin/branchA
git push origin branchB
（branchB -> branchAのPRのFiles changedが更新されていることを確認）
```
