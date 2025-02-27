# Git Lesson

## リモートリポジトリとローカルリポジトリとはそれぞれ何でしょうか？
- **リモートリポジトリ**
  - ネットワーク上に存在するリポジトリ（例: GitHub, GitLab, Bitbucket など）
  - チームでの共同開発やバックアップとして利用
  - 主な操作:
    - `git clone`：リモートリポジトリをローカルにコピー
    - `git push`：ローカルの変更をリモートに送信
    - `git pull`：リモートの変更をローカルに取り込む

- **ローカルリポジトリ**
  - 自分のPC内にあるリポジトリ
  - コードの編集やバージョン管理を行う
  - 主な操作:
    - `git init`：新しいローカルリポジトリを作成
    - `git add`：変更をステージングエリアに追加
    - `git commit`：変更を確定して履歴に保存
    - `git status`：現在のリポジトリの状態を確認
　-



## プッシュとマージの違いは何でしょうか？
- **プッシュ（push）**
  - ローカルリポジトリの変更をリモートリポジトリに送信する操作
  - コードを共有し、他の開発者が取得できるようにする
  - 主なコマンド:  
    ```sh
    git push origin ブランチ名
    ```

- **マージ（merge）**
  - 異なるブランチの変更を統合する操作
  - 例えば、新機能を開発したブランチをメインブランチに統合する場合に使用
  - 主なコマンド:  
    ```sh
    git merge ブランチ名
    ```
  - コンフリクト（競合）が発生する場合があり、手動で解決が必要なこともある


## コミットとプッシュの違い
- **コミット（commit）**
  - 自分のパソコンのリポジトリに変更を保存する
  - 例えるなら「ノートにメモを書く」イメージ
  - インターネットは不要
  - 主なコマンド:
    ```sh
    git commit -m "変更内容"
    ```

- **プッシュ（push）**
  - コミットした変更をネット上のリポジトリ（GitHub など）に送る
  - 例えるなら「書いたノートを先生に提出する」イメージ
  - インターネットが必要
  - 主なコマンド:
    ```sh
    git push origin ブランチ名
    ```



## コミットのメッセージはどのように書いてあげるのが最適でしょうか？

- **コミットメッセージの最適な書き方**
  - **簡潔でわかりやすく**（何を変更したのか一目でわかる）
  - **現在形または命令形で書く**（例: "Add login feature"）
  - **変更の意図を伝える**（なぜその変更をしたのか補足すると良い）

- **良いコミットメッセージの例**
  - `Fix typo in README`
  - `Add validation to user registration form`
  - `Update styles for better mobile responsiveness`
  - `Refactor authentication logic to improve security`

- **悪いコミットメッセージの例**
  - `Update`（何を更新したのかわからない）
  - `Fix`（何を修正したのかわからない）
  - `変更を反映`（日本語でも具体的に書くのが望ましい）

- **コミットメッセージのフォーマット例**
  - **単一行メッセージ**
    ```sh
    git commit -m "Fix bug in login validation"
    ```
  - **詳細な説明を含める場合**
    ```sh
    git commit -m "Fix bug in login validation" -m "Fixed issue where users could submit empty passwords"
    ```


## ローカルでマージするフローと、プルリクエストでマージするフローの違いは何でしょうか？
- **ローカルでマージするフロー**
  - 自分のPC上でブランチを統合する方法
  - 主に一人で作業するときや、リモートに送る前にマージしたいときに使用
  - **手順**
    1. `git checkout main`（メインブランチに移動）
    2. `git merge feature-branch`（作業ブランチを統合）
    3. `git push origin main`（リモートに反映）

- **プルリクエストでマージするフロー**
  - GitHubやGitLabなどのプラットフォーム上でコードレビューを経てマージする方法
  - チーム開発でよく使われ、他の人に確認してもらってから統合する
  - **手順**
    1. `git push origin feature-branch`（作業ブランチをリモートに送る）
    2. GitHubなどでプルリクエスト（PR）を作成
    3. レビューを受け、問題なければマージボタンを押す
    4. `git pull origin main`（ローカルにも最新の状態を反映）



## コンフリクトを起こしてしまった場合、どう対処すべきですか？
- **コンフリクト（Conflict）が起こる原因**
  - 同じファイルの同じ部分を別のブランチで変更し、マージやプルを行ったときに発生
  - 例えば、AさんとBさんが `main.js` の同じ行を変更してマージしようとすると、Gitがどちらを採用すべきか判断できずコンフリクトが発生する

- **コンフリクトの対処方法**
  1. **コンフリクトが発生したことを確認**
     ```sh
     git status
     ```
     - `Unmerged paths` と表示されているファイルがコンフリクト中

  2. **コンフリクトが発生したファイルを開く**
     - コンフリクトがある箇所は以下のように表示される
       ```txt
       <<<<<<< HEAD
       // 自分の変更
       =======
       // 相手の変更
       >>>>>>> feature-branch
       ```
  
  3. **どの変更を採用するか決める**
     - `HEAD` 側（自分の変更）を残す
     - `feature-branch` 側（相手の変更）を残す
     - 両方を組み合わせる
     - 不要な `<<<<<<<` `=======` `>>>>>>>` を削除し、正しいコードに修正
  
  4. **修正後に変更をステージング**
     ```sh
     git add コンフリクトが発生したファイル
     ```

  5. **コンフリクト解決後にコミット**
     ```sh
     git commit -m "Resolve conflict in main.js"
     ```

  6. **リモートリポジトリに反映**
     ```sh
     git push origin ブランチ名
     ```

- **コンフリクトを防ぐためのコツ**
  - こまめに `git pull` して最新の状態を保つ
  - 大きな変更をする場合はチームと相談しながら進める
  - 1つのファイルを複数人で同時に編集するのを避ける
