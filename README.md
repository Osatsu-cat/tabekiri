# 「食べきりくん」とは

賞味期限を登録すると、当日と設定日にリマインドするLINEbotです。
![pan](https://user-images.githubusercontent.com/51403845/63081689-3c019800-bf7f-11e9-8759-a9e778b5f066.png)
<img width="207" alt="QR" src="https://user-images.githubusercontent.com/51403845/63081696-415ee280-bf7f-11e9-93b4-a3db345df183.png">


## 入力画面

![tabekiri_1](https://user-images.githubusercontent.com/51403845/63081599-f6dd6600-bf7e-11e9-8e59-a61aea837509.gif)
![tabekiri_2](https://user-images.githubusercontent.com/51403845/63081609-fd6bdd80-bf7e-11e9-95f8-0bf6598ef0ec.gif)
 - 賞味期限の登録
 - 登録の確認
 - 登録の削除
 - 材料によるレシピ検索
 が行えます。

※同じ商品名につき、登録は1つまでです。
※レシピ検索は材料1つを入力してください


## リマインド画面

![tabekiri_3](https://user-images.githubusercontent.com/51403845/63081654-1b394280-bf7f-11e9-9c3c-1ee98f133cf2.gif)
 - 設定日時の朝9時にリマインドします。


# 環境
  - ruby 2.5.1
  - rails 5.2.3
  - herokuにデプロイ中


# 作成経緯
個人的に忘れがちな賞味期限の確認を、アプリケーションで解決しようと作成しました。  
また、ふと気が付いた時にすぐに入力したり、リマインドを忘れていても目につきやすいように、頻繁に利用するLINEを使用した形にしました。 

# 工夫した点
 - 連続した会話のようになるよう、ユーザーごとの最終メッセージを保存しました。メッセージ内容から会話を予測してレスポンスを送っています。
 - heroku schedulerによってタスクを管理し、ユーザーからのリクエストなしに自動でリマインドを送れるようにしています。
 - LINEのリッチメニューを使用し、ユーザー入力を極力減らしています。
 - UX向上のため、試験的に楽天APIによるレシピ検索を導入しています。


# 今度改善したい点
 - heroku schedulerがUTC基準のため、AM9時以前の設定だと日時指定がずれる現状です。日本時間基準で齟齬が出ないよう調整を予定しています。
 - herokuの場合立ち上がりに時間がかかるため、AWSに移行を検討しています。
 - レシピ検索は、厳密にはカテゴリ名との一致でレシピを取得しているため、該当率が低い現状です。スクレイピングによるレシピ検索を検討中です。