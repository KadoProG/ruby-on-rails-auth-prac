# Ruby on Rails 認証関連の構築練習

最終 Goal: **Rails 単体でユーザ認証機能のアプリケーションを作成する**

- ユーザの CRUD、適当なアプリ（TODO アプリまたは掲示板）を作成
- ユーザのログインステータスによって、表示内容を変える
- ある程度テストコードも充実させる
- やらないこと
  - MySQL、Docker など、高度な環境構築はやらない
  - API モードは使用しない

参考： [Ruby on Rails(初級編) いっしー@Web エンジニア](https://youtube.com/playlist?list=PLA4Zk0DFNhtFrRXUsnWCpX73szb5KKYun&si=6BYYN5xk_bxFTyh0)

## 作業過程

- `rails new .` で環境構築
  - ruby → 3.4.2, rails → 8.0.2
- Memo という モデルを作成
  - `rails g model Memo`
  - あとは自分で `db/migrate/〇〇_create_memos.rb`に必要なスキーマを追加
    - id は自動付与されるらしい
  - Laravel と異なり、この時点で schema.db, models ファイルなどが自動生成される
  - 今回の環境は SQLite3 なので、`storage/development.sqlite3` の内容を見れば確認できる
- Controller 作成
  - `rials g controller Memos index`
    - model は単数形なのに、controller は複数形なんですね（まあ動画が間違ってるのかもしれないが）
  - routes の `get memos/index`を以下に書き換える
    ```rb
    root :to => 'memos#index'
    resources :memos, only: [:index, :update, :destroy, :create]
    ```
