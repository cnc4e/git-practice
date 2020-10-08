[TOP](../README.md)   
前: [ブランチを切り替え忘れて開発を進めてしまった場合](./stash.md)  
次: -

---

# 3. 特定シチュエーションでの操作
## 3-7. コミットへのタグ付け
`git tag`を使うことでコミットにタグを付けることができます。主にリリースバージョンをタグとして付けることが多いです。コミットにタグが付けられていると、後から特定のコミットを探し出すことが簡単になったり、GitLabの機能でリリースページを作ったりできます。  

1. `http://ec2-54-65-130-40.ap-northeast-1.compute.amazonaws.com/container/git-practice-target.git`をクローンしてください。
2. ローカルブランチ「3-7-<社員番号>」を新しく作成し、切り替えてください。
3. ファイル「3-7.txt」を新しく作成し、コミットしてください。（コミットのコメントは何でも構いません）
4. コミットにタグ「v1.0.0-<社員番号>」を付けてください。（ヒント：注釈付きのタグを付けてみましょう。コメントは何でも構いません）
5. ブランチをプッシュしてください。リモートのブランチ名はローカルのブランチ名と同じにします。
6. タグをプッシュしてください。
7. ブラウザで[GitLab git-practice-target Tags](http://ec2-54-65-130-40.ap-northeast-1.compute.amazonaws.com/container/git-practice-target/-/tags)にアクセスし、手順4で付けたタグが表示されていることを確認してください。
8. 同じページでタグ右横のEditボタン（鉛筆マーク）をクリックし、以下の内容を入力して保存します。
   ```
   # 更新内容
   - ファイル追加
   ```
9. ブラウザで[GitLab git-practice-target Releases](http://ec2-54-65-130-40.ap-northeast-1.compute.amazonaws.com/container/git-practice-target/-/releases)にアクセスし、手順7で入力した内容が表示されることと、下部のコミットIDをクリックし手順3のコミットが表示されることを確認してください。これでリリースしたいコミットをリリースページに載せられるようになりました。
10. ブラウザで[GitLab git-practice-target Tags](http://ec2-54-65-130-40.ap-northeast-1.compute.amazonaws.com/container/git-practice-target/-/tags)にアクセスし、手順4で付けたタグを削除してください。
11. ブラウザで[GitLab git-practice-target branches](http://ec2-54-65-130-40.ap-northeast-1.compute.amazonaws.com/container/git-practice-target/-/branches)にアクセスし、手順5でプッシュしたリモートのブランチを削除してください。誤って他のブランチを削除しないようにしてください。
12. ターミナルでタグを削除してください。
13. masterブランチに切り替え、ローカルブランチ「3-7-<社員番号>」を削除してください。

--- 

[TOP](../README.md)   
前: [ブランチを切り替え忘れて開発を進めてしまった場合](./stash.md)  
次: -