[TOP](../README.md)   
前: -  
次: [Gitの設定](./gitconfig.md)  

---

# 1. 事前準備
## 1-1. インストール
それではGitをインストールします。  
Git-practiceではGitのバージョンは問いませんが、2.0.0以降を推奨します。  

使用するOSによってインストール手順に違いがあるため、自身の環境に合わせて選択してください。また、WSL（Windows Subsystem for Linux）の一部ディストリビューションではデフォルトでインストールされている場合があります。  

本項ではOSがLinuxの場合とWindowsの場合について解説します。  

### Linuxの場合
1. ターミナルで各パッケージマネージャーを使用してインストールしてください。  

apt-getが使用できる場合は、以下のコマンドを実行してください。  
`sudo apt-get install git`  

yumが使用できる場合は、以下のコマンドを実行してください。  
`sudo yum install git`  

2. `git --version`を実行し、Gitがインストールされたことを確認してください。以下のような出力になります。
```
git version 2.17.1
```

### Windowsの場合
1. ブラウザで[Git for Windows](https://git-scm.com/download/win)へアクセスしてください。インストーラのダウンロードが始まります。
2. インストーラを起動してください。オプションはすべてデフォルトのままで構いません。`Next`をクリックし、インストールを進めてください。
3. コマンドプロンプトまたはPowerShellで`git --version`を実行し、Gitがインストールされたことを確認してください。以下のような出力になります。
```
git version 2.28.0.windows.1
```

--- 

[TOP](../README.md)   
前: -  
次: [Gitの設定](./gitconfig.md)  