[TOP](../README.md)   
前: [.gitignoreと.gitkeep](./ignore-keep.md)  
次: [コミットへのタグ付け](./tag.md)  

---

# 3. 特定シチュエーションでの操作
## 3-6. ブランチを切り替え忘れて開発を進めてしまった場合
基本的にはブランチを切り替えた状態で開発作業を進めますが、うっかり切り替え忘れて進めてしまうこともあるかと思います。また、コミットするほど作業はしていないが作業状況を残しておきたい場合もあるかと思います。  
`git stash`を使うことでコミット前の変更を一時的に退避することができます。退避した内容はどのブランチにいても戻すことが可能です。
なおコミット済みの内容やリモートブランチへプッシュ済みの内容には効果がありません。あくまでローカルブランチでコミット前の内容にのみ使えます。  

1. コマンドプロンプトまたはPowerShellより、任意のディレクトリで`ターゲットリポジトリのクローンURL`を使いクローンしてください。  
なお、既にクローンしている場合はプルを行ってください。
2. mainブランチでファイル`3-6.txt`を新しく作成します。
3. 変更内容をステージングします。
4. コミット前の変更を一時的に退避します。（ヒント：引数は不要です。）
5. ローカルブランチ`3-6`を新しく作成し、切り替えます。
6. 現在のブランチを確認します。以下のようにブランチ`3-6`が選択されていることを確認してください。（他のブランチがリストされていても構いません）
```
* 3-6
main
```
7. 一時的に退避した変更のリストを表示し、stash名を確認します。（ヒント：`stash@{0}: WIP on main: a6258bf add file`のようなリストが表示されます。stash名とは`stash@{0}`の部分を指します）
8. 先ほど確認したstash名を使い、一時的に退避した変更を戻します。（ヒント：PowerShellで操作している場合はstash名をダブルクォートで囲む必要があります。）
9. ローカルブランチ`3-6`にファイル`3-6.txt`が存在していることを確認してください。
10.  mainブランチに切り替え、ローカルブランチ`3-6`を削除します。
11.  ファイル`3-6.txt`を削除します。

<details>
<summary>
答え(一例です)
</summary>

1. 
ディレクトリにターゲットリポジトリクローンがない場合
```
> git clone {ターゲットリポジトリのクローンURL}
```
既にディレクトリにターゲットリポジトリクローンがある場合
```
> git switch main
> git pull
```

2. ファイル・ディレクトリの作成はGUIでも可能なため省略
3. 
```
> git add .
```

4. 
```
> git stash
```

5. 
```
> git branch 3-6
> git switch 3-6
```

6. 
```
> git branch
  1-README
* 3-6
  3-ADDFILE
  main
```

7. 
```
> git stash list
stash@{0}: WIP on main: 9de2237 Merge pull request #3 from kato-pra/3-ADDFILE
```

8. 
PowerShellを使っている場合
```
git stash apply "stash@{0}"
```
PowerShell以外の場合
```
git stash apply stash@{0}
```

9. ファイル・ディレクトリの確認はGUIでも可能なため省略
10. 
```
> git switch main
A       3-6.txt
Switched to branch 'main'
Your branch is up to date with 'origin/main'.
> git branch -D 3-6
Deleted branch 3-6 (was 9de2237).
```

11. ファイル・ディレクトリの削除はGUIでも可能なため省略

</details>

--- 

[TOP](../README.md)   
前: [.gitignoreと.gitkeep](./ignore-keep.md)  
次: [コミットへのタグ付け](./tag.md)  