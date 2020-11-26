# cheer-talk

## アプリケーション概要
チャットを通じて他者の相談に乗る、応援することに焦点を当てたアプリ
## 利用方法
アカウントを作成後、部屋を作成あるいは既存の部屋に入室しチャットが可能になる
## 目指した課題解決
気軽に悩みを解決したい、話したいがカウンセリングや専門機関への相談が難しい、
気が乗らないことから行動に移せない人の問題解決、より気軽に相談できる場所の提供を
目的としている
## 洗い出した用件
- 
## 実装した機能についての説明
- 新規登録をすることで以下の各種機能が利用できる
- ログイン、ログアウト機能
- room作成機能
名前を設定し、会話のためのroomが作成できる

## 実装予定の機能
- 相談に乗ったユーザーをいいねボタン等で評価する機能
- 評価に伴いランクが上がる機能
- チャットとは別で個別に送れるメッセージ機能
- 
## データベース設計
- https://gyazo.com/5e3062d953b915f5ca0f23191ef1317b

## ローカルでの動作方法
以下の手順でコマンドを行う。
- clone
- bundle install
- yarn install
- rails db:create
- rails db:migrate
- rails s
- http://localhost:3000/にアクセスする

# テーブル設計

## users テーブル

| Column   | Type   | Options     |
| -------- | ------ | ----------- |
| name     | string | null: false |
| email    | string | null: false |
| password | string | null: false |
| birthday | date   | null: false |

### Association

- has_many :room_users
- has_many :talk_rooms, through: room_users
- has_many :messages

## talk_rooms テーブル

| Column | Type   | Options     |
| ------ | ------ | ----------- |
| name   | string | null: false |

### Association

- has_many :room_users
- has_many :users, through: room_users
- has_many :messages

## room_users テーブル

| Column | Type       | Options                        |
| ------ | ---------- | ------------------------------ |
| user   | references | null: false, foreign_key: true |
| room   | references | null: false, foreign_key: true |

### Association

- belongs_to :talk_room
- belongs_to :user

## messages テーブル

| Column  | Type       | Options                        |
| ------- | ---------- | ------------------------------ |
| content | string     |                                |
| user    | references | null: false, foreign_key: true |
| room    | references | null: false, foreign_key: true |

### Association

- belongs_to :talk_room
- belongs_to :user
