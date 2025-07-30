[TOP](../README.md)   
前: [マージ時の競合解決](./conflict.md)  
次: [.gitignoreと.gitkeep](./ignore-keep.md)  

---

# 3. 特定シチュエーションでの操作
## 3-4. コミットの取消・打消
コミットの取消と打消について取り上げます。コミットの取消とは、対象コミット自体を無かったことにしコミット履歴を前の状態に戻すことを指します。コミットの打消とは、対象コミットの変更内容を元に戻すコミットを作成することを指します。この場合コミット履歴には変更を元に戻すコミットが追加され、対象コミットはそのまま残ります。  
`git reset`を使うことでコミットを取り消すことができます。このコマンドはオプションによって、コミットのみ取消、コミットおよびインデックスの取消、コミット・インデックス・手元ファイルの変更の取消と挙動が変わります。現在の状況に適したオプションを使うようにしましょう。なおリモートブランチにプッシュ済みの内容に対して`git reset`を使っても、プッシュ時にエラーになります。その場合はコミットの取消ではなく打消を行いましょう。  
`git revert`を使うことでコミットを打ち消すことができます。

1. コマンドプロンプトまたはPowerShellより、任意のディレクトリで`ターゲットリポジトリのクローンURL`を使いクローンしてください。  
なお、既にクローンしている場合はプルを行ってください。
2. ローカルブランチ`3-4`を新しく作成し、切り替えてください。
3. 現在のブランチを確認します。以下のようにブランチ`3-4`が選択されていることを確認してください。（他のブランチがリストされていても構いません）
```
* 3-4
main
```
4. ファイル`3-4.txt`を新しく作成し、コミットしてください。（コミットのコメントは何でも構いません）
5. コミットの履歴を確認してください。
6. 直前のコミットのみ取り消してください。（ヒント：`--soft`オプションを使い、対象コミットは`HEAD^`を指定します）
7. コミットの履歴を確認し、直前のコミットが取り消されているのを確認してください。
8. コミットしてください。（ヒント：インデックスの状態はそのままなので、コミットするだけで構いません）
9. 直前のコミット・インデックス・手元ファイルの変更を取り消してください。（ヒント：`--hard`オプションを使い、対象コミットは`HEAD^`を指定します）
10. コミットの履歴・インデックスの状態・手元ファイルをそれぞれ確認し、直前のコミットに関わる部分が取り消されているのを確認してください。
11. ファイル`3-4.txt`を再度作成し、コミットしてください。（コミットのコメントは何でも構いません）
12. 直前のコミットを打ち消してください。コマンド実行後コミットのコメント編集画面を閉じる（:wqで閉じられます）と処理が実行されます。（ヒント：対象コミットは`HEAD`を指定します）
13. コミットの履歴を確認し、直前のコミットが残っていることおよび変更を元に戻すコミットが追加されていることを確認してください。以下のようなコミットが追加されています。
```
commit 5a9c719ce7fa20155f30a5a804c334b1a8830902 (HEAD -> 3-4)
Author: xx xx <xxxxx.xxx@xxxx.xx.xx>
Date:   Wed Dec 9 00:49:35 2020 +0000

Revert "add file"
    
This reverts commit 07014855a7559d1959ac2b0f84d03a7ca6c48eae.

commit 07014855a7559d1959ac2b0f84d03a7ca6c48eae
Author: xx xx <xxxxx.xxx@xxxx.xx.xx>
Date:   Wed Dec 9 00:47:33 2020 +0000

add file
```
14.  mainブランチに切り替え、ローカルブランチ`3-4`を削除してください。

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
> git branch 3-4
> git switch 3-4
Switched to branch '3-4'
```

3. 
```
> git branch
  1-README
* 3-4
  3-ADDFILE
  main
```

4. ファイルの作成はGUIでも可能なため省略
```
> git add .
> git commit -m "sample"
[3-4 6edf1ed] sample
 1 file changed, 0 insertions(+), 0 deletions(-)
 create mode 100644 3-4.txt
```

5. 
```
> git log
commit 6edf1ed4fa451ff5625dac6ca3ca0afd0e03d18f (HEAD -> 3-4)
Author: kato-pra <kato.kenta@tis.co.jp>
Date:   Wed Jun 25 18:17:17 2025 +0900

    sample

commit 9de2237c3381b2104b7fa99f88ed08a4e5db98d2 (origin/main, origin/3-1, main)
Merge: ae05a9d c52f40f
Author: kato-pra <139187218+kato-pra@users.noreply.github.com>
Date:   Thu Jun 19 19:57:33 2025 +0900

    Merge pull request #3 from kato-pra/3-ADDFILE

    #3 add file
```

6. 
```
> git reset --soft HEAD^
```

7. 
```
> git log
commit 9de2237c3381b2104b7fa99f88ed08a4e5db98d2 (HEAD -> 3-4, origin/main, origin/3-1, main)
Merge: ae05a9d c52f40f
Author: kato-pra <139187218+kato-pra@users.noreply.github.com>
Date:   Thu Jun 19 19:57:33 2025 +0900

    Merge pull request #3 from kato-pra/3-ADDFILE

    #3 add file
```

8. 
```
> git commit -m "sample"
[3-4 7ca33ca] sample
 1 file changed, 0 insertions(+), 0 deletions(-)
 create mode 100644 3-4.txt
```

9. 
```
> git reset --hard HEAD^
HEAD is now at 9de2237 Merge pull request #3 from kato-pra/3-ADDFILE
```

10. 
```
コミット履歴
> git log
commit 9de2237c3381b2104b7fa99f88ed08a4e5db98d2 (HEAD -> 3-4, origin/main, origin/3-1, main)
Merge: ae05a9d c52f40f
Author: kato-pra <139187218+kato-pra@users.noreply.github.com>
Date:   Thu Jun 19 19:57:33 2025 +0900

    Merge pull request #3 from kato-pra/3-ADDFILE

    #3 add file

インデックスの状態
> git status
On branch 3-4
nothing to commit, working tree clean

手元ファイル
> ls


    ディレクトリ: C:\Users\tie308747\Documents\git-test\git-practice-target


Mode                 LastWriteTime         Length Name
----                 -------------         ------ ----
-a----        2025/06/19     19:59              0 Must.txt
-a----        2025/06/19     19:24              0 README.md
```

11. プラクティス4と同じ操作のため省略
12. 
```
> git revert HEAD
[3-4 b85f21c] Revert "sample"
 1 file changed, 0 insertions(+), 0 deletions(-)
 delete mode 100644 3-4.txt

エディタ画面が出てきた場合、:を押下した後にwqと入力してください
```

13. 
```
> git log
commit b85f21cc776532c38ff3d2f477bec619a84db794 (HEAD -> 3-4)
Author: kato-pra <kato.kenta@tis.co.jp>
Date:   Wed Jun 25 18:35:51 2025 +0900

    Revert "sample"

    This reverts commit b4e9d9b8e86b814f1ee57730df79a627324d002f.

commit b4e9d9b8e86b814f1ee57730df79a627324d002f
Author: kato-pra <kato.kenta@tis.co.jp>
Date:   Wed Jun 25 18:35:43 2025 +0900

    sample

commit 9de2237c3381b2104b7fa99f88ed08a4e5db98d2 (origin/main, origin/3-1, main)
Merge: ae05a9d c52f40f
Author: kato-pra <139187218+kato-pra@users.noreply.github.com>
Date:   Thu Jun 19 19:57:33 2025 +0900

    Merge pull request #3 from kato-pra/3-ADDFILE

    #3 add file
```

14. 
```
> git switch main
Switched to branch 'main'
Your branch is up to date with 'origin/main'.
> git branch -D 3-4
Deleted branch 3-4 (was b85f21c).
```

</details>

--- 

[TOP](../README.md)   
前: [マージ時の競合解決](./conflict.md)  
次: [.gitignoreと.gitkeep](./ignore-keep.md)  
