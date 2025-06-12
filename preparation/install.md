[TOP](../README.md)   
前: -  
次: [Gitの設定](./gitconfig.md)  

---

# 1. 事前準備
## 1-1. インストール
それではGitをインストールします。  
Git-practiceではGitのバージョンは問いませんが、**2.0.0**以降を推奨します。  

使用するOSによってインストール手順に違いがあるため、自身の環境に合わせて選択してください。また、WSL（Windows Subsystem for Linux）の一部ディストリビューションではデフォルトでインストールされている場合があります。  

本項ではOSがLinuxの場合とWindowsの場合について解説します。  

### Linuxの場合
1. ブラウザで[Git](https://git-scm.com/download/linux)へアクセスしてください。各OSにおけるインストール手順が解説されています。
2. ターミナルで各パッケージマネージャーを使用してインストールしてください。  

apt-get（Debian/Ubuntu等）を使う場合は、以下のコマンドを実行してください。  
`sudo apt-get install git`  

yum（CentOS/RHEL等）を使う場合は、以下のコマンドを実行してください。  
`sudo yum install git`  

その他の場合は、手順1のサイトを参考にインストールしてください。

3. `git --version`を実行し、Gitがインストールされたことを確認してください。以下のような出力になります。
```
git version 2.17.1
```

### Windowsの場合
1. ブラウザで[Git for Windows](https://git-scm.com/download/win)へアクセスしてください。インストーラのダウンロードが始まります。
2. ダウンロードしたインストーラを起動してください。オプションはすべてデフォルトのままで構いません。`Next`をクリックし、インストールを進めてください。
3. コマンドプロンプトまたはPowerShellで`git --version`を実行し、Gitがインストールされたことを確認してください。以下のような出力になります。
```
git version 2.28.0.windows.1
```

--- 

[TOP](../README.md)   
前: -  
次: [Gitの設定](./gitconfig.md)  