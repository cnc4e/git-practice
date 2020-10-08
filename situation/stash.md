[TOP](../README.md)   
前: [.gitignoreと.gitkeep](./ignore-keep.md)  
次: [コミットへのタグ付け](./tag.md)  

---

# 3. 特定シチュエーションでの操作
## 3-6. ブランチを切り替え忘れて開発を進めてしまった場合
基本的にはブランチを切り替えた状態で開発作業を進めますが、うっかり切り替え忘れて進めてしまうこともあるかと思います。また、コミットするほど作業はしていないが作業状況を残しておきたい場合もあるかと思います。  
`git stash`を使うことでコミット前の変更を一時的に退避することができます。退避した内容はどのブランチにいても戻すことが可能です。  
なおコミット済みの内容やリモートブランチへプッシュ済みの内容には効果がありません。あくまでローカルブランチでコミット前の内容にのみ使えます。  

1. `http://ec2-54-65-130-40.ap-northeast-1.compute.amazonaws.com/container/git-practice-target.git`をクローンしてください。
2. masterブランチでファイル「3-6.txt」を新しく作成します。
3. 変更内容をステージングします。
4. コミット前の変更を一時的に退避します。（ヒント：引数は不要です。）
5. ローカルブランチ「3-6」を新しく作成し、切り替えます。
6. 一時的に退避した変更を戻します。（ヒント：PowerShellで操作している場合はstash名をダブルクォートで囲む必要があります。）
7. ローカルブランチ「3-6」にファイル「3-6.txt」が存在していることを確認してください。
8. masterブランチに切り替え、ローカルブランチ「3-6」を削除します。
9. ファイル「3-6.txt」を削除します。


--- 

[TOP](../README.md)   
前: [.gitignoreと.gitkeep](./ignore-keep.md)  
次: [コミットへのタグ付け](./tag.md)  