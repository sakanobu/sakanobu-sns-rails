## ワークフロー

1. 手順
   1. GitHub で 「Issues」 → 「New issue」とクリックし、  
      「Title」という欄に日本語で `ToDo の一覧を返す API の作成` などと簡潔に書きつつ、  
      「Leave a comment」を `## 概要` `## 想定するユーザーの挙動`  
       `## 期待するシステムの挙動` `## その他` などで埋めたり、  
       右サイドにある、「Assignees」「Labels」「Milestone」なども付与しつつ、
      「Submit new issue」をクリック
      - 先にローカルでブランチを切るのではなく、  
        今後の作業に関する思考の整理も兼ねて GitHub で Issue を立てに行ったほうが良さげ
   1. ローカルに戻り、`git fetch origin main`
      - 僕の Mac の bash の補完だと何故か `git fetch origin main:main` となるので注意  
        いつか直したいね
   1. `git rebase origin/main main`
   1. `git checkout -b all_todo_return_api/#x`
      - x には Issue の「Title」の右横に表示される数字を記述
   1. `git commit --allow-empty -m "[WIP] ToDo の一覧を返す API の作成 #x"`
      - この最初のコミットの名前が Issue の Title と被るのって粒度の問題なのかな？  
         別に Issue と Pull request が一対一に対応するのが絶対ではないし…
   1. `git push origin all_todo_return_api/#x`
   1. GitHub のリポジトリのホーム画面で強調されている「Compare & pull request」をクリックし、  
      「Leave a comment」を `## 概要` `## 設計の方針`  
       `## 関連する Issue や Pull request\n\nToDo の一覧を返す API の作成 #x`  
       `## その他` `## タスク` などで埋めたり、  
       右サイドにある、「Reviewers」「Assignees」「Labels」「Milestone」なども付与しつつ、  
       その後「Create pull request」をクリック
   1. ちょこちょこローカルで `git add ○○` → `git commit -m "△△"` していく
      - 実際の開発では WIP でも他の人がチラ見できるようにちょこちょこリモートに push したほうが良さそう
   1. レビューできるところまでやり終えたら、`git rebase -i HEAD~y` して  
      rebase -i の vim の画面で HEAD~y-1 番目の冒頭を "edit" にして vim を抜け、  
      `git commit --allow-empty --amend -m "ToDo の一覧を返す API の作成 #x"` と "[WIP]" を消し、  
      `git rebase --continue` をする
   1. 歴史の改変をローカルで行ったので、`git fetch origin main` をまずして、  
      次に `git push --force-with-lease origin all_todo_return_api/#x` をして、  
      今までのローカルのコミットを全てリモートにあげる
   1. GitHub の Pull requests に移動し、  
       該当のプルリクを選択し、  
       タイトル横の「Edit」ボタンを押し [WIP] という記述を削除し「Save」をし、  
      「Merge pull request」ボタンを押し、そこで表示されるコメント欄に `close #x` と上書きし  
       「Confirm merge」ボタンをクリックし、  
       更にそのままの画面ですぐ下に現れる「Delete branch」をクリックしてリモートのブランチを消してしまう
   1. ローカルに戻ってきて、`git checkout main`
   1. `git fetch origin main`
   1. `git rebase origin/main main`
   1. `git branch -d all_todo_return_api/#x`
      - 場合によっては `git remote prune origin` をしてリモートでは消されているはずのブランチがローカルで依然として表示されている事態に対処

### その他重要テーマ

1. イベント系エンティティに思い至るのってどのタイミングなんだ…
1. 業務フローについて
   - 参考
     1. [【新人プログラマ応援】開発タスクをアサインされたらどういう手順で進めるべきか - Qiita](https://qiita.com/jnchito/items/017487cd882091494298)
