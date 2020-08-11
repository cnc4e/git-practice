# git-practice
## 1. はじめに
## 1-1. Gitについて
## 1-2. Gitを使うメリット
## 1-3. インストール
## 1-4. 事前準備
- Gitのプロキシ
- Gitのユーザ/メールアドレス

## 2. 基礎
Gitの基礎について学びます。  
2-1から2-3では用語とコマンドを覚えながらGitを扱っていきます。  

## 2-1. ローカルでコミット

### 今回やることの図

```mermaid
sequenceDiagram
participant A as 手元のファイル
participant B as インデックス
participant C as ローカルリポジトリ
A->>B: ステージング
B->>C: コミット
Note over C: コミットを蓄積
```

### 用語
#### ローカルリポジトリ
自分のマシン上でファイルやディレクトリの状態を記録する場所です。ファイルやディレクトリの変更履歴が格納されます。

#### コミット
ファイルやディレクトリの追加・変更をリポジトリに記録する操作です。操作を行うと、ローカルリポジトリに前回コミットから現在までの差分を記録します。記録された差分の情報のこともコミットと呼びます。

#### インデックス（ステージング）
ファイルやディレクトリを変更した後、コミットの対象とするファイルやディレクトリを登録しておくものをインデックスと呼びます。インデックスに登録する操作をステージングと呼びます。  
インデックスに登録されていないファイルやディレクトリはコミットされないため、コミットを行う前にステージングを行う必要があります。  


### プラクティス
任意のディレクトリで`git init`を実行するとそのディレクトリはローカルリポジトリの管理下に置かれます。ファイルを変更した後、`git add`を実行するとファイルの変更はインデックスに登録されます。`git commit`を実行するとインデックスに登録された内容をコミットとしてローカルリポジトリに記録します。  
なお、`git status`を実行するとインデックスの状態を確認できます。`git log`を実行するとコミットの履歴を確認できます。

1. 任意の位置にディレクトリ「git-practice-local」を作成してください。（手段は問いません）
2. コマンドプロンプトまたはPowerShellでcdコマンドを実行し、ディレクトリ「git-practice-local」へ移動してください。
3. 「git-practice-local」をGitのローカルリポジトリ管理下に初期化してください。
4. ファイル「2-1.txt」を作成してください。（手段は問いません）
5. すべてのファイルをステージングしてください。
6. インデックスの状態を確認してください。以下のような出力になり、ファイル「2-1.txt」がインデックスに記録されていることを確認してください。
```
On branch master

No commits yet

Changes to be committed:
  (use "git rm --cached <file>..." to unstage)
        new file:   2-1.txt
```
7. コメント「first commit」をつけてコミットしてください。
8. インデックスの状態を確認してください。以下のような出力になり、ファイル「2-1.txt」がインデックスから消えていることを確認してください。
```
On branch master
nothing to commit, working tree clean
```
9. コミットの履歴を確認してください。以下のような出力になり、ローカルリポジトリにコミットが記録されていることを確認してください。
```
commit e24bd3e10037e21b1619f596979c450516633313 (HEAD -> master)
Author: xx xx <xxxxx.xxx@tis.co.jp>
Date:   Tue Jul 28 11:38:51 2020 +0900

    first commit
```

ここまでの内容で、ローカルリポジトリにコミットを記録していくことができるようになりました。コミットが記録されていることで、容易に特定時点のファイル内容を復元できます。個人で開発する場合はローカルリポジトリへの記録で構いませんが、多人数で開発する場合はリモートリポジトリへ記録していくことになります。次項ではリモートリポジトリを交えたGitの使い方を学んでいきます。

## 2-2. リモートにプッシュ
### 今回やることの図

```mermaid
sequenceDiagram
participant A as 手元のファイル
participant B as インデックス
participant C as ローカルリポジトリ
participant D as リモートリポジトリ
D->>C: クローン
A->>B: ステージング
B->>C: コミット
Note over C: 1.<br>コミットを蓄積
C->>D: プッシュ
Note over D: 2.<br>複数人のコミットを蓄積<br>コミットを共有
D->>C: プル
Note over C: 3.<br>コミットを取込
```

### 用語
#### リモートリポジトリ
共有サーバ上でファイルやディレクトリの状態を記録する場所です。

#### クローン
リモートリポジトリを複製し、ローカルリポジトリを作成する操作です。ファイルやディレクトリがダウンロードされるのに加え、変更履歴も複製されます。

#### プッシュ
ローカルリポジトリの変更履歴をアップロードし、リモートリポジトリを更新する操作です。

#### プル
リモートリポジトリの変更履歴をダウンロードし、ローカルリポジトリを更新する操作です。

### プラクティス
`git clone`を実行することでリモートリポジトリの既存プロジェクトを手元にクローンすることができます。クローンしたファイルに変更を加え、`git push`でリモートリポジトリへ変更履歴をアップロードしてみます。その後、他の人がリモートリポジトリのファイルを更新した体で`git pull`を実行し、手元のローカルリポジトリを更新してみます。  
GitLabからログインを求められた場合は、以下のユーザ/パスワードを使用してください。  
git-practice/git-practice  

1. コマンドプロンプトまたはPowerShellを使い、任意のディレクトリで`http://ec2-54-65-130-40.ap-northeast-1.compute.amazonaws.com/cicd-study-group/git-practice-target.git`をクローンしてください。
2. cdコマンドを実行し、ディレクトリ「git-practice-target」へ移動してください。
3. ファイル「<社員番号>.txt」を作成してください。（手段は問いません。自身の社員番号をファイル名にしてください）
4. すべてのファイルをステージングしてください。
5. コメント「add file」をつけてコミットしてください。
6. リモートリポジトリを更新してください。リポジトリは`origin`、ブランチは`master`です。以下のような出力になることを確認してください。
```
Enumerating objects: 4, done.
Counting objects: 100% (4/4), done.
Delta compression using up to 8 threads
Compressing objects: 100% (2/2), done.
Writing objects: 100% (3/3), 284 bytes | 284.00 KiB/s, done.
Total 3 (delta 0), reused 0 (delta 0), pack-reused 0
To http://ec2-54-65-130-40.ap-northeast-1.compute.amazonaws.com/cicd-study-group/git-practice-target.git
   30bd289..0dea3af  master -> master
```
7. ブラウザで[GitLab git-practice-target](http://ec2-54-65-130-40.ap-northeast-1.compute.amazonaws.com/cicd-study-group/git-practice-target)にアクセスしてください。先ほどプッシュした内容が反映され、手順3で作成したファイルがリモートリポジトリに追加されていることを確認してください。
8. [GitLab git-practice-target](http://ec2-54-65-130-40.ap-northeast-1.compute.amazonaws.com/cicd-study-group/git-practice-target)の「＋マーク > New file」をクリックしてください。ファイル名を「<社員番号>-extra.txt」とし、「Commit changes」をクリックしてください。（内容は適当で構いません）
9. コマンドプロンプトまたはPowerShellを使い、ローカルリポジトリを更新してください。以下のような出力になることを確認してください。
```
remote: Enumerating objects: 3, done.
remote: Counting objects: 100% (3/3), done.
remote: Compressing objects: 100% (2/2), done.
remote: Total 2 (delta 0), reused 0 (delta 0), pack-reused 0
Unpacking objects: 100% (2/2), 268 bytes | 11.00 KiB/s, done.
From http://ec2-54-65-130-40.ap-northeast-1.compute.amazonaws.com/cicd-study-group/git-practice-target
   0dea3af..abe1aae  master     -> origin/master
Updating 0dea3af..abe1aae
Fast-forward
 <社員番号>-extra.txt | 0
 1 file changed, 0 insertions(+), 0 deletions(-)
 create mode 100644 <社員番号>-extra.txt
```
10.  実際にファイルを開いたり、コミットの履歴を確認したりして、リモートリポジトリに対して行われた変更が手元に反映されていることを確認してください。
11.  手順3・手順8で作成したファイルを削除してください。（手段は問いません）
12.  すべてのファイルをステージングし、コメント「delete files」をつけてコミットし、リモートリポジトリを更新してください。リポジトリは`origin`、ブランチは`master`です。
13.  ブラウザで[GitLab git-practice-target](http://ec2-54-65-130-40.ap-northeast-1.compute.amazonaws.com/cicd-study-group/git-practice-target)にアクセスしてください。先ほどプッシュした内容が反映され、手順3・手順8で作成したファイルがリモートリポジトリから削除されていることを確認してください。

ここまでの内容で、リモートリポジトリを用いて複数人で開発をすることができるようになりました。手元で変更した内容は適宜コミットし、ある程度コミットが溜まったらリモートリポジトリにプッシュします。コミットやプッシュの粒度はプロジェクトによって決められている場合が多いため、指針がある場合はそれに従ってください。  
リモートリポジトリを用いた開発を学習しましたが、実際の開発作業では複数の機能追加やリリースバージョンが並行して存在する場合が多々あります。その際、複数の変更履歴が混在してしまうと全容の把握が難しくなります。次項では「ブランチ」という概念を学び、この問題点を解決します。

## 2-3. ブランチを分ける
### 今回やることの図

![](./assets/2-3-1.drawio.svg)

### 用語
#### ブランチ
コミットを分岐して記録できるようにするものです。ローカル・リモート問わずリポジトリ作成時にはmasterブランチが存在しています。

#### マージ
分岐したブランチを他のブランチと合流させる操作のことです。

#### issue
プロジェクトにおけるタスクのことです。機能開発やバグ対応などをissueとして書き出しておき、issueごとにブランチを作成してタスクを実行することで、タスクとコードを紐づけて管理することができます。
なおGitに備わった仕組みではなく、GithubやGitLabなどリモートリポジトリ機能を持つサービスに備わった仕組みです。  

#### プルリクエスト/マージリクエスト
ブランチをマージする際、変更点を確認できる仕組みです。レビューに使うことができます。  
なおGitに備わった仕組みではなく、GithubやGitLabなどリモートリポジトリ機能を持つサービスに備わった仕組みです。Githubではプルリクエスト、GitLabではマージリクエストと呼びます。

### プラクティス

GitLabのissueを確認します。issueに紐づく新しいブランチを`git checkout -b`で作成し、issueに従って変更を行います。その後、作成したブランチをリモートリポジトリへプッシュし、マージリクエスト機能を使ってみます。  
なお、`git branch`を実行するとブランチ一覧と現在のブランチを確認できます。  
GitLabからログインを求められた場合は、以下のユーザ/パスワードを使用してください。  
git-practice/git-practice  

1. ブラウザで[GitLab git-practice-target issue#1](http://ec2-54-65-130-40.ap-northeast-1.compute.amazonaws.com/cicd-study-group/git-practice-target/-/issues/1)にアクセスし、内容を確認してください。
2. コマンドプロンプトまたはPowerShellを使い、任意のディレクトリで`http://ec2-54-65-130-40.ap-northeast-1.compute.amazonaws.com/cicd-study-group/git-practice-target.git`をクローンしてください。（[2-2](#2-2-リモートにプッシュ)で実行している場合は不要です）
3. cdコマンドを実行し、ディレクトリ「git-practice-target」へ移動してください。（[2-2](#2-2-リモートにプッシュ)で実行している場合は不要です）
4. ローカルリポジトリのブランチ一覧を確認し、以下のような出力になることを確認してください。
```
* master
```
5. 新しいブランチ「1」を作成してください。
6. ローカルリポジトリのブランチ一覧を確認し、以下のような出力になることを確認してください。
```
* 1
  master
```
7. issueの対応内容に従い、ファイル「<社員番号>.txt」を作成してください。（手段は問いません。自身の社員番号をファイル名にしてください）
8. すべてのファイルをステージングし、コメント「add file」をつけてコミットしてください。
9. リモートリポジトリを更新してください。リポジトリは`origin`、ローカルブランチは`1`、リモートブランチは`1`です。（コマンドの書き方は「git ブランチ指定」などで検索してください）以下のような出力になることを確認してください。
```
Enumerating objects: 4, done.
Counting objects: 100% (4/4), done.
Delta compression using up to 8 threads
Compressing objects: 100% (2/2), done.
Writing objects: 100% (3/3), 312 bytes | 312.00 KiB/s, done.
Total 3 (delta 0), reused 0 (delta 0), pack-reused 0
remote:
remote: To create a merge request for issue#1, visit:
remote:   http://ec2-54-65-130-40.ap-northeast-1.compute.amazonaws.com/cicd-study-group/git-practice-target/-/merge_requests/new?merge_request%5Bsource_branch%5D=1
remote:
To http://ec2-54-65-130-40.ap-northeast-1.compute.amazonaws.com/cicd-study-group/git-practice-target.git
 * [new branch]      1 -> 1
```
9. ブラウザで[GitLab git-practice-target branches](http://ec2-54-65-130-40.ap-northeast-1.compute.amazonaws.com/cicd-study-group/git-practice-target/-/branches)にアクセスし、先ほど作成したブランチ「1」がリモートリポジトリにプッシュされていることを確認してください。
10. ブランチ「1」右側の「Merge request」ボタンをクリックし、以下の内容でマージリクエストを作成してください。入力後、「Submit merge request」ボタンをクリックしてください。 
```
Title: #1 テキストファイル編集
Description:
# 関連するIssue
cicd-study-group/git-practice-target#1

# MRの内容
- テキストファイル「<社員番号>.txt」を作成

```
11. 「Merge」ボタンをクリックし、ブランチ「1」をmasterブランチにマージしてください。（本当はレビュー担当者またはマージ担当者にマージ作業を分担します）
12. ブラウザで[masterブランチ](http://ec2-54-65-130-40.ap-northeast-1.compute.amazonaws.com/cicd-study-group/git-practice-target/-/blob/master/)の内容を確認し、先ほど編集したファイルがmasterブランチに反映されていることを確認してください。

ここまでの内容で、ブランチとissueについて学ぶことができました。これにより、実際のプロジェクトにおいても複数人と並行して開発作業を行うことができるようになります。  

## 3-1.
## 3-2.