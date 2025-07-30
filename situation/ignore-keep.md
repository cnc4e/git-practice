[TOP](../README.md)   
前: [コミットの取消・打消](./reset-revert.md)  
次: [ブランチを切り替え忘れて開発を進めてしまった場合](./stash.md)  

---

# 3. 特定シチュエーションでの操作
## 3-5. .gitignoreと.gitkeep
開発作業には必要でも、Gitに登録したくないファイルは多々あると思います。例えば接続用の鍵ファイルや、大量に生成されるログファイル・一時ファイルなどがそれにあたります。このような場合はリポジトリのルートディレクトリに`.gitignore`というファイルを作成しGitに登録しておくことで、任意のファイルを登録対象から除外することができます。  
また、Gitは空のディレクトリを管理しません。例えばアプリケーションに必要なディレクトリを空にしていた場合、Gitには登録されていないため、ビルドが失敗する可能性があります。このような場合は、登録したいディレクトリに`.gitkeep`というファイルを作成しておくことで、空のディレクトリをGitの管理下におくことが慣習になっています。

1. コマンドプロンプトまたはPowerShellより、任意のディレクトリで`ターゲットリポジトリのクローンURL`を使いクローンしてください。  
なお、既にクローンしている場合はプルを行ってください。
2. 新しいブランチ`3-5-ignore`を作成し、切り替えてください。
3. 現在のブランチを確認します。以下のようにブランチ`3-5-ignore`が選択されていることを確認してください。（他のブランチがリストされていても構いません）
```
* 3-5-ignore
main
```
4. リポジトリのルートディレクトリ配下にファイル`3-5.pem`・ディレクトリ`3-5-log`を作成し、ディレクトリ`3-5-log`配下にファイル`3-5-ignore.log`を作成してください。
5. インデックスの状態を確認し、手順4で作成したファイルが`Untracked files:`として表示されていることを確認してください。
6. リポジトリのルートディレクトリ配下にファイル`.gitignore`を以下の内容で作成してください。
```
*.pem
/3-5-log/*.log
```
7. インデックスの状態を確認し、手順4で作成したファイルが`Untracked files:`として表示されていないことを確認してください。（手順5で作成したファイル`.gitignore`は表示されます。）これにより手順3で作成したファイルはステージングももちろんコミットもされない状態になります。
8. 手順4と手順6で作成したファイル・ディレクトリを削除してください。
9. mainブランチに切り替え、ローカルブランチ`3-5-ignore`を削除してください。
10. 新しいブランチ`3-5-keep`を作成し、切り替えてください。
11. 現在のブランチを確認します。以下のようにブランチ`3-5-keep`が選択されていることを確認してください。（他のブランチがリストされていても構いません）
```
* 3-5-keep
main
```
12. リポジトリのルートディレクトリ配下にディレクトリ`3-5-necessary`を作成してください。
13. インデックスの状態を確認し、手順12で作成した空のディレクトリが`Untracked files:`として表示されていないことを確認してください。
14. ディレクトリ`3-5-necessary`配下にファイル`.gitkeep`を作成してください。
15. インデックスの状態を確認し、手順12で作成した空のディレクトリが`Untracked files:`として表示されていることを確認してください。これにより空のディレクトリをGitの管理下におくことができます。
16. 手順12と手順14で作成したファイル・ディレクトリを削除してください。
17. mainブランチに切り替え、ローカルブランチ`3-5-keep`を削除してください。

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

2. 
```
> git branch 3-5-ignore
> git switch 3-5-ignore
Switched to branch '3-5-ignore'
```

3. 
```
> git branch
  1-README
* 3-5-ignore
  3-ADDFILE
  main
```

4. ファイル・ディレクトリの作成はGUIでも可能なため省略
5. 
```
> git status
On branch 3-5-ignore
Untracked files:
  (use "git add <file>..." to include in what will be committed)
        3-5-log/
        3-5.pem

nothing added to commit but untracked files present (use "git add" to track)
```

6. ファイルの作成はGUIでも可能なため省略
7. 
```
> git status
On branch 3-5-ignore
Untracked files:
  (use "git add <file>..." to include in what will be committed)
        .gitignore

nothing added to commit but untracked files present (use "git add" to track)
```

8. ファイル・ディレクトリの削除はGUIでも可能なため省略
9. 
```
> git switch main
Switched to branch 'main'
Your branch is up to date with 'origin/main'.
> git branch -D 3-5-ignore
Deleted branch 3-5-ignore (was 9de2237).
```

10. 
```
> git branch 3-5-keep
> git switch 3-5-keep
Switched to branch '3-5-keep'
```

11. 
```
> git branch
  1-README
* 3-5-keep
  3-ADDFILE
  main
```

12. ディレクトリの作成はGUIでも可能なため省略
13. 
```
> git status
On branch 3-5-keep
nothing to commit, working tree clean
```

14. ファイルの作成はGUIでも可能なため省略
15. 
```
> git status
On branch 3-5-keep
Untracked files:
  (use "git add <file>..." to include in what will be committed)
        3-5-necessary/

nothing added to commit but untracked files present (use "git add" to track)
```

16. ファイル・ディレクトリの削除はGUIでも可能なため省略
17. 
```
> git switch main
Switched to branch 'main'
Your branch is up to date with 'origin/main'.
> git branch -D 3-5-keep
Deleted branch 3-5-keep (was 9de2237).
```

</details>

--- 

[TOP](../README.md)   
前: [コミットの取消・打消](./reset-revert.md)  
次: [ブランチを切り替え忘れて開発を進めてしまった場合](./stash.md)  