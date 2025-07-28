[TOP](../README.md)   
前: [リモートリポジトリのブランチを取得](./fetch.md)  
次: [マージ時の競合解決](./conflict.md)  

---

# 3. 特定シチュエーションでの操作
## 3-2. 他のブランチをマージ
同時並行で開発作業が進んでいる場合、他の人の作業を取り込んで手元でテストや動作確認を行いたいシーンが出てきます。`git merge`を使うことで、他のブランチの内容を自分が作業しているブランチに反映させることができます。  

1. コマンドプロンプトまたはPowerShellより、任意のディレクトリで`ターゲットリポジトリのクローンURL`を使いクローンしてください。
2. ブラウザで`ターゲットリポジトリのページ`にアクセスし、「main」プルダウンから`Find or create branch...`にブランチ名を入力し、「Create branch: <ブランチ名>」からリモートリポジトリに新しいブランチを作成してください。ブランチ名は`3-2-remote`とします。
3. 「Add file」ボタンより、ブランチ`3-2-remote`にファイル`3-2-remote.txt`を作成してください。
4. コマンドプロンプトまたはPowerShellより、リモートリポジトリのブランチを取得してください。
5. 新しいブランチ`3-2-local`を作成し、切り替えてください。
6. 現在のブランチを確認します。以下のようにブランチ`3-2-local`が選択されていることを確認してください。（他のブランチがリストされていても構いません）
```
* 3-2-local
main
```
7. ブランチ`3-2-local`にファイル`3-2-local.txt`を作成してください。
8. リモートのブランチ`3-2-remote`を現在のブランチ`3-2-local`にマージしてください。（ヒント：リモートのブランチ名は`origin/3-2-remote`になります）
9. ルートディレクトリに`3-2-remote.txt`と`3-2-local.txt`が存在していることを確認してください。
10. そのままブランチ`3-2-local`でコミットしてください。（コミットしない場合、mainブランチまでファイルが引き継がれてしまいます）
11. mainブランチに切り替えてください。
12. 先ほど作成したブランチ`3-2-local`を削除してください。
13. ブラウザで`ターゲットリポジトリのページ`にアクセスし、「main」プルダウン右横の「branches」より、手順2で作成したリモートのブランチを削除してください。

ディレクトリや別名ファイルは問題なくマージされます。また、同じファイルでも異なる行であれば特に操作を行うことなくマージされます。  

次のプラクティスでは、同じファイルの同じ行を更新していた場合の競合を解決する操作を行います。

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

2. 3-1のプラクティス2の操作と同じです。そちらを参考にしてください。
3. 2-2のプラクティス9の操作と同じです。そちらを参考にしてください。
4. 
```
> git fetch
remote: Enumerating objects: 4, done.
remote: Counting objects: 100% (4/4), done.
remote: Compressing objects: 100% (2/2), done.
remote: Total 3 (delta 0), reused 0 (delta 0), pack-reused 0 (from 0)
Unpacking objects: 100% (3/3), 945 bytes | 85.00 KiB/s, done.
From https://github.com/kato-pra/git-practice-target
 * [new branch]      3-2-remote -> origin/3-2-remote
```

5. 
```
> git branch 3-2-local
> git switch 3-2-local
Switched to branch '3-2-local'
```

6. 
```
> git branch
  1-README
* 3-2-local
  3-ADDFILE
  main
```

7. ファイル作成はGUIでも可能なため省略  
なお、この差分をコミットした後にmainブランチに切り替えると、GUIからもファイルが見えなくなります

8. 
```
> git merge origin/3-2-remote
Updating 9de2237..a52a5be
Fast-forward
 3-2-remote.txt | 1 +
 1 file changed, 1 insertion(+)
 create mode 100644 3-2-remote.txt
```

9. 
```
> ls


    ディレクトリ: C:\Users\tie308747\Documents\git-test\git-practice-target


Mode                 LastWriteTime         Length Name
----                 -------------         ------ ----
-a----        2025/06/24     17:51              0 3-2-local.txt
-a----        2025/06/24     17:53              2 3-2-remote.txt
-a----        2025/06/19     19:59              0 Must.txt
-a----        2025/06/19     19:24              0 README.md
```

10. 
```
> git add .
> git commit -m "3-2 commit"
[3-2-local a5407ee] 3-2 commit
 1 file changed, 0 insertions(+), 0 deletions(-)
 create mode 100644 3-2-local.txt
```
なお、ここのコミットメッセージは任意です

11. 
```
> git switch main
Switched to branch 'main'
Your branch is up to date with 'origin/main'.
```

12. 
```
> git branch -D  3-2-local
Deleted branch 3-2-local (was a5407ee).
```

13. 3-1のプラクティス8の操作と同じです。参考にしてください。

</details>

--- 

[TOP](../README.md)   
前: [リモートリポジトリのブランチを取得](./fetch.md)  
次: [マージ時の競合解決](./conflict.md)  