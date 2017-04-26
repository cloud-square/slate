---
title: ChatSquare API

language_tabs:

toc_footers:
  - <a href='#'>Sign Up for a Developer Key</a>
  - <a href='https://github.com/tripit/slate'>Documentation Powered by Slate</a>

includes:
  - errors

search: true
---


# スキーマ

## Card

クレジットカード情報

カラム名 | 型 | NOT NULL | 説明
--- | --- | --- | ---
payjp_card_id | String | ✓| PayjpのCard ID
user_id | String | ✓| 作成者
group_id | String | ✓| グループ
expire_year | String | | 期限年
expire_month | String | | 期限月
brand | String | | カードブランド
last4 | String| | 最後の下4桁
digit| Integer | | カード桁数
is_default | Json | | 決済で使用するカード

## Comment

コメント情報

カラム名 | 型 | NOT NULL | 説明
--- | --- | --- | ---
room_id | String | ✓| ルーム
grouop_user_id | String | ✓| 作成者
text | Text | ✓| テキスト
link_comment | Json | | リンクコメント
re_comment | Json | | 返信コメント
attachments | Json | | 添付ファイル
tags | Json| | タグ情報
emojis| Json | | リアクション情報
tos | Json | | 宛先情報
parent | Json | | 返信コメント群
to_all | Boolean | ✓| 全員に当てたものか
is_deleted | Boolean |✓ | 論理削除フラグ
room_comment_ofset | Integer | | ルームのコメントの中でのoffset

## CommentFile

コメントの添付ファイル情報

カラム名 | 型 | NOT NULL | 説明
--- | --- | --- | ---
upload_file_id| String | ✓ | ファイル
room_id| String | ✓ | コメントのルーム
comment_id | String | ✓| コメント
room_folder_id | String | | 保存フォルダ

## CommentTag

コメントのタグ情報

カラム名 | 型 | NOT NULL | 説明
--- | --- | --- | ---
room_id| String | ✓ | コメントのルーム
comment_id | String | ✓| コメント
tag_id | String | ✓| タグ

## CommentTo

コメントの宛先情報

カラム名 | 型 | NOT NULL | 説明
--- | --- | --- | ---
room_id| String | ✓ | コメントのルーム
comment_id | String | ✓| コメント
group_user_id | String | ✓| 宛先

## Group

グループ情報

カラム名 | 型 | NOT NULL | 説明
--- | --- | --- | ---
group_id | String | ✓| グループ
name | String | ✓| グループ名
status | Integer | ✓| 0: プラン加入中 <br>1: トライアル中<br>2:  トライアル終了<br>3: 無料<br>7: 課金失敗<br>8: 削除<br>9: ロック中
user_plan_name | String | ✓| ユーザプラン名
file_plan_name | String | ✓| ファイルプラン名
storage_usage | Bigint |✓ | ストレージ使用量
is_deleted | Boolean | ✓| 論理削除フラグ
trial_ended_at| Datetime | ✓| トライアル終了日時
avatar_url | Text | | アバターURL

## GroupUser

グループメンバー情報

カラム名 | 型 | NOT NULL | 説明
--- | --- | --- | ---
group_id | String | ✓| グループ
user_id | String | ✓| ユーザ
name | String | ✓| メンバー名
yomi | String | | 読み
role | Integer | ✓| 0: master<br>1: admin<br>2: member<br>3: guest
storage_usage | Bigint |✓ | ストレージ使用量
max_storage_usage | Bigint| ✓| アップロード可能ファイル容量
avatar_url| Text | | アバターURL
sub_group_ids | Json | | 所属サブグループ情報
email | String |✓ | グループにおけるメールアドレス
status | Integer | ✓| 0: 招待中 <br>1: 参加中

* `status`: 招待時に招待メールアドレスに紐づくUserがまだいない場合は0、いる場合は1、グループの作成者は初期値1。0の間はパスワードをリセットして招待メールを再送信できる。招待ユーザの初回ログイン時に1に変わる。

## InformationEmail

お知らせ受信用メールアドレス

カラム名 | 型 | NOT NULL | 説明
--- | --- | --- | ---
group_id| String | ✓ | グループ
email | String | ✓| メールアドレス

## Log

ログ情報

カラム名 | 型 | NOT NULL | 説明
--- | --- | --- | ---
group_id | String | | 操作ユーザのグループ
user_id | String | | 操作ユーザ
controller_name | String | | コントローラ名
action_name | String | | アクション名
http_method | String | | HTTPメソッド名
request_url | Text | | リクエストURL
request_params | Json | | リクエストパラメータ
response_content_type| String | | レスポンスのコンテントタイプ
http_status_code | String | | レスポンスステータスコード
user_agent | Text | | ユーザエージェント
app_version | String | | アプリバージョン
os | String | | 端末OS
referrer | Text | | リファラー
error_class | String | | エラークラス
error_message | Text | | エラーメッセージ
error_backtrace | Text | | エラー内容
request_time | Datetime | ✓| リクエスト日時
response_time | Datetime | ✓| レスポンス日時
execute_time | Float | ✓| 処理実行時間

## PayjpCustomer

Payjpの顧客情報

カラム名 | 型 | NOT NULL | 説明
--- | --- | --- | ---
id| String | ✓ | PayjpのCustomer ID
user_id | String | ✓| プラン購入者
group_id | String | ✓| グループ

## Plan

プラン情報

カラム名 | 型 | NOT NULL | 説明
--- | --- | --- | ---
name | String | ✓| プラン名
amount | String | ✓| 料金
product_type | String | ✓| user: ユーザ数<br>file: ファイル容量
count | Bigint | | プラン適用値
payjp_id | String |✓ | PayjpのPlan ID
trial | Boolean | ✓| トライアルプランかどうか
sort | Boolean | ✓| 表示順


## ReadLater

「あとで読む」に登録したコメント情報

カラム名 | 型 | NOT NULL | 説明
--- | --- | --- | ---
group_user_id | String | ✓| 登録したグループユーザ
room_id | String | ✓| 登録したコメントのルーム
comment_id | String |✓ | 登録したコメント

## Room

ルーム情報

カラム名 | 型 | NOT NULL | 説明
--- | --- | --- | ---
user_id | String | ✓| 作成者
group_id | String | ✓| 所属グループ
name | String | ✓| ルーム名
description | Text | | 説明
type | String |✓ |group: グループチャット<br>pair: ダイレクトチャット<br>private: マイルーム|
comment_count | Integer | ✓| 総コメント数
is_deleted | Boolean | ✓| 論理削除フラグ
storage_usage | Bigint | ✓| 使用ストレージ量
avatar_url | Text | | アバターURL

## RoomFolder

ファイルの保存先フォルダ情報

カラム名 | 型 | NOT NULL | 説明
--- | --- | --- | ---
group_user_id | String | ✓| 作成者
room_id | String | ✓| 所属ルーム
name | String |✓ | フォルダ名
parent_id | String | | 親フォルダ

## RoomMember

ルームメンバー情報

カラム名 | 型 | NOT NULL | 説明
--- | --- | --- | ---
user_id | String | ✓| 所属ユーザ
group_user_id | String | ✓| 所属グループメンバー
room_id | String | ✓| 所属ルーム
role | Text |✓ | 0: 管理者<br>1: 一般
unread_count | Integer |✓ |未読コメント数|
to_count | Integer | ✓| 未読の自分宛コメント数
re_count | Integer | ✓| 未読の自分宛返信コメント数
read_later_count | Integer | ✓| 「あとで読む」の数
unread_comment_offset | Integer | | 最後の未読コメント番号
snoozed_at | Datetime | | スヌーズに設定した日

## SubGroup

サブグループ情報

カラム名 | 型 | NOT NULL | 説明
--- | --- | --- | ---
user_id | String | ✓| 作成者
group_id | String | ✓| 所属グループ
name | String |✓ | サブグループ名

## Subscription

現在のプラン購読情報

カラム名 | 型 | NOT NULL | 説明
--- | --- | --- | ---
group_id | String | ✓| GroupのID
payjp_user_subscription_id | String | | PayjpのSubscription ID
payjp_file_subscription_id | String | | PayjpのSubscription ID

## Tag

タグ情報

カラム名 | 型 | NOT NULL | 説明
--- | --- | --- | ---
group_user_id | String | ✓| 作成者
room_id | String |✓ | 作成したRoomのID
color_code | String | ✓| カラーコード
name | String |✓ | タグ名

## UploadFile

ユーザがアップロードしたファイル情報

カラム名 | 型 | NOT NULL | 説明
--- | --- | --- | ---
group_user_id | String | ✓| アップロード者
name | String | ✓| ファイル名
size | Bigint | ✓| ファイルサイズ
content_type| String| ✓| コンテントタイプ
width | Integer | | 幅
height | Integer | | 高さ
thumbnail_width | Integer | | サムネイルの幅
thumbnail_height | Integer | | サムネイルの高さ
is_uploaded |Boolean| | アップロード完了/未完了
thumbnail_url | Text | | サムネイルURL
thumbnail_updated_at | Datetime | | サムネイルのURLの最終更新日

## User

ユーザ情報

カラム名 | 型 | NOT NULL | 説明
--- | --- | --- | ---
email | String | ✓| メールアドレス
password_hash | String | ✓|ハッシュ化されたパスワード
password_digit | Integer | ✓| パスワード桁数
language| String| ✓| 言語 |
last_group_id | String | | 最後に表示したGroupのID
preview_mode | Boolean | ✓| プレビューモードのON/OFF
last_signed_in_at | Datetime | | 最終ログイン日
last_access_at | Datetime | | 最終アクセス日
done_guide | Json | ✓| 閲覧済みガイド
status | Integer | ✓| 0: ログイン前<br>1: ログイン済み<br>9: 削除
type | Integer | ✓| 0: 一般ユーザ<br>1: サポートメンバー<br>2: システムメンバー

## UserConfirmation

新規登録入力情報

カラム名 | 型 | NOT NULL | 説明
--- | --- | --- | ---
email | String | ✓| メールアドレス
name | String | ✓| ユーザ名
group_name | String | ✓| グループ名

## UserMail

ユーザに送信したメール情報

カラム名 | 型 | NOT NULL | 説明
--- | --- | --- | ---
email | String | ✓| 宛先メールアドレス
user_id | String | ✓| 送信対象のユーザ
purpose | String | ✓| reset_password: パスワード再設定<br>change_email: メールアドレス変更|
is_deleted | Boolean |✓ | 論理削除フラブ


# アカウント

## アカウントを新規登録

アカウントを新規登録します。

### HTTP Request

`POST /user_confirmations`

### Parameters

パラメータ名 | 型 | 必須 | 詳細
--------- | ------- | ------- | -----------
name | String | ✓| 名前
email | String | ✓| メールアドレス
group_name | String | ✓| グループ名

> レスポンスなし

## メールアドレス認証

アカウントを新規登録後にメール認証します。

### HTTP Request

`PUT /user_confirmations/:id`

### Parameters

パラメータ名 | 型 | 必須 | 詳細
--------- | ------- | ------- | -----------
password | String | | パスワード

<aside class="notice">
メール認証のリンクをクリックする時は password なし
</aside>

> レスポンスなし

## 認証メール再送信

認証メールを再送信します。

### HTTP Request

`POST /user_confirmations/resend_register_email`

### Parameters

パラメータ名 | 型 | 必須 | 詳細
--------- | ------- | ------- | -----------
email | String | ✓ | メールアドレス

> レスポンスなし

## アカウント情報変更

アカウント情報を変更します。

### HTTP Request

`PUT /users/:id`

### Parameters

パラメータ名 | 型 | 必須 | 詳細
--------- | ------- | ------- | -----------
email | String | | メールアドレス
password | String | | パスワード
preview_mode | Boolean | | プレビューモードのON/OFF

> レスポンスなし






# セッション

## ログイン

### HTTP Request

`POST /sessions`

### Parameters

パラメータ名 | 型 | 必須 | 詳細
--------- | ------- | ------- | -----------
email | String | ✓| メールアドレス
password | String | ✓| パスワード

> レスポンスなし


## ログアウト

### HTTP Request

`DELETE /sessions/:id`

### Parameters

なし

> レスポンスなし





# グループ

## グループ一覧を取得

自分の所属しているグループ情報を取得します。

また、表示対象のグループ情報、、サブグループ情報、メンバー情報も取得します。

パラメータに`gt`を付与することで、表示対象のグループを指定することができます。指定しなかった場合は、最後に表示されたグループを自動的に表示対象にします。


### HTTP Request

`GET /api/v1/groups`

### Parameters

パラメータ名 | 型 | 必須 | 詳細
--------- | ------- | ------- | -----------
gt | String | | グループID

> レスポンス

```ruby

{
  groups: {
    [
      {
        id: "db6fff7e-c9c8-4aad-a1d4-787888a13f2c",
        name: "CloudSquare",
        avatar_url: "https://...",
      },
      {
        id: "222b7ca1-335b-449d-ace2-4c783b40d854",
        name: "CloudSquare2",
        avatar_url: "https://..."
      }
    ]
  },
  current_group: {
    id: "db6fff7e-c9c8-4aad-a1d4-787888a13f2c",
    name: "CloudSquare",
    user_plan: { name: "user_10", count: 10, display_name: null　},
    file_plan: { name: "file_30", count: 30, display_name: "30 GB" },
    avatar_url: "https://...",
    status: 0,
    receive_information_emails: ["sample1@exapmle.com", "sample2@exapmle.com"],
    storage_usage_limit_readable: 3 GB,
    storage_usage_rate: 33,
    storage_usage_readable: 1 GB,
    group_users: {
      [
        {
          id: "9103bfde-4169-4a22-a78d-d4218ceeea37",
          name: "User A",
          yomi: "",
          role: "normal",
          sub_group_ids: ["b7af7802-38e4-4bbe-9bee-2d7da3812362", "3e148b83-c8cf-4c9d-88ad-7a2651341cc7"],
          avatar_url: "https://...",
          email: "user_a@example.com"
        },
        {
          id: "ce5ba1d7-b256-4a17-a85b-0c8b1fa8ef0d",
          name: "User B",
          yomi: "",
          role: "master",
          sub_group_ids: [],
          avatar_url: "https://...",
          email: "user_b@example.com"
        }
      ]
    }
    sub_groups: {
      [
        {
          id: "b7af7802-38e4-4bbe-9bee-2d7da3812362",
          name: "sub_group_a"
        },
        {
          id: "3e148b83-c8cf-4c9d-88ad-7a2651341cc7",
          name: "sub_group_b"
        }
      ]
    }
  },
  current_group_user: {
    id: "ce5ba1d7-b256-4a17-a85b-0c8b1fa8ef0d",
    name: "User B",
    yomi: "",
    role: "master",
    sub_group_ids: [],
    avatar_url: "https://...",
    email: "user_b@example.com",
    password_digit: "8",
    language: "ja",
    preview_mode: true,
    done_guide: ["popup_comment"]
  }
}
```

### HTTP Response: groups

ユーザが所属するグループ一覧が配列として含まれます。

キー名 | 型 | 詳細
--------- | ------- | -----------
id | String | グループID
name | String | グループ名
avatar_url | String | アバターのURL<br>（未設定ならnull）

### HTTP Response: current_group

表示対象のグループ情報が含まれます。

キー名 | 型  | 詳細
--------- | ------- | -----------
id | String |  グループID
name | String |  グループ名
user_plan | Json | ユーザプラン情報<br>（master・adminのみ）
file_plan | Json | ファイルプラン情報<br>（master・adminのみ）
avatar_url | String | アバターのURL<br>（未設定ならnull）
status | Integer | 0: 有料プラン加入中 <br> 1: トライアル中 <br> 2: トライアル期間終了<br> 3: 課金失敗<br> 8: 退会<br> 9: ロック中
receive_information_emails | Array | お知らせ受信メールアドレス<br>（masterのみ）
storage_usage_limit_readable | String | ストレージ使用上限<br>（masterのみ）
storage_usage_readable | String | 現在のストレージ使用量<br>（masterのみ）
storage_usage_rate | Integer | 現在のストレージ使用率<br>（masterのみ）


`group_users`: グループのメンバー情報が配列として含まれます。

キー名 | 型 | 詳細
--------- | ------- | -----------
id | String | メンバーID
name | String | メンバー名
yomi | String | メンバー名のよみ
role | String | グループ内の権限
avatar_url | String | アバターのURL<br>（未設定ならnull）
email | String | メールアドレス
sub_group_ids | Array | 所属するサブグループID<br>（無所属なら空の配列）

`sub_groups`: 所属しているサブグループ一覧が配列として含まれます。

### HTTP Response: current_group_user

表示対象のグループの自分のメンバー情報と、全グループ共通のユーザ情報が含まれます。

キー名 | 型 | 詳細
--------- | ------- | -----------
id | String | メンバーID
name | String | メンバー名
yomi | String | メンバー名のよみ
role | String | グループ内の権限
avatar_url | String | アバターのURL<br>（未設定ならnull）
email | String | メールアドレス
sub_group_ids | Array | 所属するサブグループID<br>（無所属なら空の配列）
password_digit | Integer | パスワード桁数
language | String | 表示言語
preview_mode | Boolean | プレビュー機能のON/OFF
done_guide | Json | 閲覧済みの操作ガイド（未操作ならnull）

## グループ情報を取得

特定のグループ情報を取得します。

### HTTP Request

`GET /api/v1/groups/me`

<aside class="notice">
masterのみ利用可能です
</aside>

### Parameters

パラメータ名 | 型 | 必須 | 詳細
--------- | ------- | ------- | -----------
gt | String | ✓| グループID

> レスポンス

```ruby
{
  id: "db6fff7e-c9c8-4aad-a1d4-787888a13f2c",
  name: "CloudSquare",
  avatar_url: "https://...",
  status: 0,
  storage_usage_rate: 45
  storage_usage_readable: "45 GB"
  storage_usage_limit_readable: "100 GB"
}
```

### HTTP Response

ユーザが所属するグループ情報が含まれます。

キー名 | 型 | 詳細
--------- | ------- | -----------
id | String | グループID
name | String | グループ名
avatar_url | String | アバターURL
status | Integer | 上記参照
storage_usage_rate | Integer | ストレージ使用率(%)
storage_usage_readable | String | ストレージ使用量
storage_usage_limit_readable| String | ストレージ上限

## グループ情報を変更

特定のグループ名を変更します。

### HTTP Request

`PUT /api/v1/groups/me`

<aside class="notice">
masterのみ利用可能です
</aside>

### Parameters

パラメータ名 | 型 | 必須 | 詳細
--------- | ------- | ------- | -----------
gt | String | ✓| グループID
name | String | ✓| グループ名

> レスポンスは GET /api/v1/groups/me と同じ

### HTTP Response

更新したグループ情報が含まれます。


# グループメンバー

## メンバーを作成

グループのメンバーを作成します。


### HTTP Request

`POST /api/v1/group_users`

<aside class="notice">
master, adminのみ操作可能です。ただし、adminはmasterの作成はできません。
</aside>


### Parameters

パラメータ名 | 型 | 必須 | 詳細
--------- | ------- | ------- | -----------
gt | String | ✓| グループID
email | String | | メールアドレス
name | String | | 名前
yomi | String | | よみ
role | String | | 権限(master, admin, member, guest)

> レスポンスは GET /api/v1/groups の group_users と同じ

### HTTP Response

更新したメンバー情報が含まれます。



## メンバー情報を更新

メンバー情報を更新します。


### HTTP Request

`PUT /api/v1/group_users/:id`

### Parameters

パラメータ名 | 型 | 必須 | 詳細
--------- | ------- | ------- | -----------
gt | String | ✓| グループID
name | String | | 名前
yomi | String | | よみ
role | String | | 権限<br>master, adminのみ操作可

> レスポンスは GET /api/v1/groups の group_users と同じ

### HTTP Response

更新したメンバー情報が含まれます。


## メンバー情報を削除

メンバー情報を削除します。APIの`/:id`に`bulk`と指定すると一括削除が可能になります。


### HTTP Request

`DELETE /api/v1/group_users/:id`

<aside class="notice">
master, adminのみ操作可能です。ただし、adminはmasterの削除はできません。
</aside>

### Parameters

パラメータ名 | 型 | 必須 | 詳細
--------- | ------- | ------- | -----------
gt | String | ✓| グループID
group_user_ids | Array | | グループユーザIDの配列。<br>idに"buld"を指定した時のみ

> レスポンスはなし

### HTTP Response

なし




# 契約情報

## 契約情報を取得

プラン一覧、加入中のプラン、クレジットカードを取得します。

### HTTP Request

`GET /api/v1/subscriptions`

### Parameters

パラメータ名 | 型 | 必須 | 詳細
--------- | ------- | ------- | -----------
gt | String | ✓| グループID


> レスポンス

```ruby

{
  plans: {
    users: {
      [
        {
          amount: 5000,
          count: 10,
          display_name: null,
          name: "user_10"
        },
        {
          amount: 10000,
          count: 20,
          display_name: null,
          name: "user_20"
        }
      ],
    }
    files: {
      [
        {
          amount: 0,
          count: 30,
          display_name: "30GB",
          name: "file_30"
        },
        {
          amount: 2000,
          count: 100,
          display_name: "100GB",
          name: "file_100"
        }
      ]
    }
  },
  default_card: {
    brand: "Visa",
    exp_month: 12,
    exp_year: 2020,
    last4: "4242"
  },
  user_plan: {
    name: "user_10",
    count: 10,
    display_name: null　
  },
  file_plan: {
    name: "file_30",
    count: 30,
    display_name: "30GB"
  },
  trial_ended_at: "2017/03/27"
}
```

### HTTP Response: default_card

<aside class="notice">
トライアル期間中はこのキーは含まれません。
</aside>

現在使用中のカード情報が含まれます。

キー名 | 型 | 詳細
--------- | ------- | -----------
id | String | カードID
brand | String | ブランド名
digit | Integer | 桁数
expire_year | String | 有効期限年
expire_month | String | 有効期限月
is_default | Boolean | 現在使用中かどうか
last4 | String | 最後の4桁

### HTTP Response: plans

ChatSquareのプラン情報一覧が含まれます。

* `users`: ユーザプラン一覧
* `files`: ファイルプラン一覧

キー名 | 型 | 詳細
--------- | ------- | -----------
name | String | プランID
amount | Integer | プラン料金
count | Integer | 適用される数値
display_name | String | 表示名。<br>ユーザプランは言語によって異なるのでnull。

### HTTP Response: user_plan

現在加入中のユーザプラン情報が含まれます。
JSONの中身は`HTTP Response: plans`と同じ

### HTTP Response: file_plan

現在加入中のファイルプラン情報が含まれます。
JSONの中身は`HTTP Response: plans`と同じ

### HTTP Response: trial_ended_at

<aside class="notice">
有料プラン加入中はこのキーは含まれません。
</aside>

トライアルが終了する日付が含まれます。


## カード情報を取得

登録済みのカード一覧を取得します。

### HTTP Request

`GET /api/v1/cards`

### Parameters

パラメータ名 | 型 | 必須 | 詳細
--------- | ------- | ------- | -----------
gt | String | | グループID

> レスポンス

```ruby
[
  {
    brand: "JCB",
    digit: 16,
    expire_month: 1,
    expire_year: 2019,
    id: "7fa0f67f-cd48-4f3e-8091-6888c0bffca5",
    is_default: true,
    last4: 0505
  }
]
```

### HTTP Response

登録済みのカード一覧の配列が含まれます。

キー名 | 型 | 詳細
--------- | ------- | -----------
id | String | カードID
brand | String | ブランド名
digit | Integer | 桁数
expire_year | String | 有効期限年
expire_month | String | 有効期限月
is_default | Boolean | 現在使用中かどうか
last4 | String | 最後の4桁

## カード情報を作成

新規カードを登録します。

### HTTP Request

`POST /api/v1/cards`

### Parameters

パラメータ名 | 型 | 必須 | 詳細
--------- | ------- | ------- | -----------
gt | String | ✓| グループID
number | String | ✓| カード番号
cvc | String | ✓| セキュリティコード
exp_year | String | ✓| 有効期限年
exp_month | String | ✓| 有効期限月

> レスポンス

```ruby
{
  brand: "JCB",
  digit: 16,
  expire_month: 1,
  expire_year: 2019,
  id: "7fa0f67f-cd48-4f3e-8091-6888c0bffca5",
  is_default: true,
  last4: 0505
}
```

### HTTP Response

登録されたカード情報が含まれます。

## 使用するカードを変更

使用するカードを変更します。

### HTTP Request

`PUT /api/v1/cards/:id`

### Parameters

パラメータ名 | 型 | 必須 | 詳細
--------- | ------- | ------- | -----------
gt | String | ✓| グループID

> レスポンス

```ruby
{
  brand: "JCB",
  digit: 16,
  expire_month: 1,
  expire_year: 2019,
  id: "7fa0f67f-cd48-4f3e-8091-6888c0bffca5",
  is_default: true,
  last4: 0505
}
```

### HTTP Response

変更したカード情報が含まれます。

## プランに加入する

初めてプランに加入するときのリクエストです。加入するプラン情報とカード情報を同時に登録します。

### HTTP Request

`POST /api/v1/subscriptions`

### Parameters

パラメータ名 | 型 | 必須 | 詳細
--------- | ------- | ------- | -----------
gt | String | ✓| グループID
number | String | ✓| カード番号
cvc | String | ✓| セキュリティコード
exp_year | String | ✓| 有効期限年
exp_month | String | ✓| 有効期限月
file_plan_name | String | ✓| プランID
user_plan_name | String | ✓| プランID


> レスポンス

```ruby
{
  user_plan: {
    name: "user_10",
    count: 10,
    display_name: null　
  },
  file_plan: {
    name: "file_30",
    count: 30,
    display_name: "30 GB"
  },
  default_card: {
    brand: "Visa",
    exp_month: 12,
    exp_year: 2020,
    last4: "4242"
  }
}

```

### HTTP Response

加入したプラン情報とカード情報が含まれます。

## プランを変更する

プラン情報を変更します。

### HTTP Request

`POST /api/v1/subscriptions`

### Parameters

パラメータ名 | 型 | 必須 | 詳細
--------- | ------- | ------- | -----------
gt | String | ✓| グループID
file_plan_name | String | ✓| プランID
user_plan_name | String | ✓| プランID


> レスポンス

```ruby
{
  user_plan: {
    name: "user_10",
    count: 10,
    display_name: null　
  },
  file_plan: {
    name: "file_30",
    count: 30,
    display_name: "30 GB"
  }
}

```

### HTTP Response

変更後のプラン情報が含まれます。





# ルーム

## ルーム一覧を取得

自分の所属しているグループ情報を取得します。

また、表示対象のグループ情報、サブグループ情報、メンバー情報も取得します。

パラメータに`gt`を付与することで、表示対象のグループを指定することができます。指定しなかった場合は、最後に表示されたグループを自動的に表示対象にします。また、
パラメータに`ct`を付与することで、表示対象のコメントを指定することができます。

### HTTP Request

`GET /api/v1/rooms`

### Parameters

パラメータ名 | 型 | 必須 | 詳細
--------- | ------- | ------- | -----------
gt | String | | グループID
ct | String | | コメントID

> レスポンス

```ruby

{
  groups: [
    {
      id: "db6fff7e-c9c8-4aad-a1d4-787888a13f2c",
      name: "CloudSquare",
      avatar_url: "https://..."
    },
    {
      id: "222b7ca1-335b-449d-ace2-4c783b40d854",
      name: "CloudSquare2",
      avatar_url: "https://..."
    }
  ],
  current_group: {
    id: "db6fff7e-c9c8-4aad-a1d4-787888a13f2c",
    name: "CloudSquare",
    user_plan: { name: "user_10", count: 10, display_name: null　},
    file_plan: { name: "file_30", count: 30, display_name: "30 GB" },
    avatar_url: "https://...",
    status: 0,
    receive_information_emails: ["sample1@exapmle.com", "sample2@exapmle.com"],
    rooms: [
      {
        description: "",
        group_user_id: "354b3d97-f4c0-4394-bfe8-4ddd2eef94ae",
        id: "9de5c180-0c1b-4466-a682-d3c7e6a40915",
        name: "room1",
        re_count: 0,
        read_later_count: 0,
        role: "manager",
        to_count: 0,
        type: "group",
        unread_count: 0,
        updated_at: 1489748431
      },
      {
        description: "",
        group_user_id: "354b3d97-f4c0-4394-bfe8-4ddd2eef94ae",
        id: "241fc360-6995-43eb-9be8-8003e43485df",
        name: "room2",
        re_count: 0,
        read_later_count: 0,
        role: "manager",
        to_count: 0,
        type: "group",
        unread_count: 0,
        updated_at: 1489748175
      }
    ],
    group_users: [
      {
        id: "9103bfde-4169-4a22-a78d-d4218ceeea37",
        name: "User A",
        yomi: "",
        role: "normal",
        sub_group_ids: ["b7af7802-38e4-4bbe-9bee-2d7da3812362", "3e148b83-c8cf-4c9d-88ad-7a2651341cc7"],
        avatar_url: "https://...",
        email: "user_a@example.com"
      },
      {
        id: "ce5ba1d7-b256-4a17-a85b-0c8b1fa8ef0d",
        name: "User B",
        yomi: "",
        role: "master",
        sub_group_ids: [],
        avatar_url: "https://...",
        email: "user_b@example.com"
      }
    ],
    sub_groups: [
      {
        id: "b7af7802-38e4-4bbe-9bee-2d7da3812362",
        name: "sub_group_a"
      },
      {
        id: "3e148b83-c8cf-4c9d-88ad-7a2651341cc7",
        name: "sub_group_b"
      }
    ]
  },
  current_group_user: {
    id: "ce5ba1d7-b256-4a17-a85b-0c8b1fa8ef0d",
    name: "User B",
    yomi: "",
    role: "master",
    sub_group_ids: [],
    avatar_url: "https://...",
    email: "user_b@example.com",
    password_digit: "8",
    language: "ja",
    preview_mode: true,
    done_guide: ["popup_comment"]
  }
}
```

### HTTP Response: groups

ユーザが所属するグループ一覧が配列として含まれます。

### HTTP Response: current_group

表示対象のグループ情報が含まれます。

`group_users`: グループのメンバー情報が配列として含まれます。

`sub_groups`: 所属しているサブグループ一覧が配列として含まれます。

`rooms`: グループで所属しているルーム情報が配列として含まれます。

キー名 | 型 | 詳細
--------- | ------- | -----------
id | String | ルームID
name | String | ルーム名
description | String | ルーム概要
group_user_id | String | 自分のメンバーID
type | String | group: グループチャット<br>pair: ダイレクトチャット<br>private: マイルーム
role | String | manager: 管理者<br>normal: 一般参加者
re_count | Integer | 未読の返信コメント数
read_later_count | Integer | 未読の「あとで読む」コメント数
to_count | Integer | 未読のToコメント数
unread_count | Integer | 未読コメント数
updated_at | Integer | ルームの更新日時<br>(UTCタイムゾーンのUNIXタイムスタンプ)


### HTTP Response: current_group_user

表示対象のグループの自分のメンバー情報と、全グループ共通のユーザ情報が含まれます。


## ルーム情報を取得

特定のルーム情報を取得します。

### HTTP Request

`GET /api/v1/rooms/:id`

### Parameters

パラメータ名 | 型 | 必須 | 詳細
--------- | ------- | ------- | -----------
gt | String | ✓| グループID

> レスポンス

```ruby

{
  description: "",
  id: "9de5c180-0c1b-4466-a682-d3c7e6a40915",
  name: "room1",
  is_manager: true,
  updated_at: 1489748431,
  type: "group",
  avatar_url: "https://...",
  comments: [
    {

    },
  ],
  tags: [
    {

    },
  ],
  room_members: [
    {
      group_user_id: "354b3d97-f4c0-4394-bfe8-4ddd2eef94ae",
      role: "normal"
    },
    {
      group_user_id: "eeef8f11-c786-4ba8-a924-ebd2bb09f78f",
      role: "manager"
    },
  ],
}
```

### HTTP Response

キー名 | 型 | 詳細
--------- | ------- | -----------
id | String | ルームID
name | String | ルーム名
description | String | ルーム概要
type | String | 上記参照
is_manager | Booelan | 管理者かどうか
updated_at | Integer | 上記参照
room_members| Array | ルームメンバー |
tags| Array |　ルームタグ|
comments| Array | コメント |

`comments`

最新のコメント一覧が含まれます。

`tags`

ルームのタグ一覧が含まれます。




# Authentication

> To authorize, use this code:

```ruby
require 'kittn'

api = Kittn::APIClient.authorize!('meowmeowmeow')
```

```python
import kittn

api = kittn.authorize('meowmeowmeow')
```

```shell
# With shell, you can just pass the correct header with each request
curl "api_endpoint_here"
  -H "Authorization: meowmeowmeow"
```

```javascript
const kittn = require('kittn');

let api = kittn.authorize('meowmeowmeow');
```

> Make sure to replace `meowmeowmeow` with your API key.

Kittn uses API keys to allow access to the API. You can register a new Kittn API key at our [developer portal](http://example.com/developers).

Kittn expects for the API key to be included in all API requests to the server in a header that looks like the following:

`Authorization: meowmeowmeow`

<aside class="notice">
You must replace <code>meowmeowmeow</code> with your personal API key.
</aside>

# Kittens

## Get All Kittens

```ruby
require 'kittn'

api = Kittn::APIClient.authorize!('meowmeowmeow')
api.kittens.get
```

```python
import kittn

api = kittn.authorize('meowmeowmeow')
api.kittens.get()
```

```shell
curl "http://example.com/api/kittens"
  -H "Authorization: meowmeowmeow"
```

```javascript
const kittn = require('kittn');

let api = kittn.authorize('meowmeowmeow');
let kittens = api.kittens.get();
```

> The above command returns JSON structured like this:

```json
[
  {
    "id": 1,
    "name": "Fluffums",
    "breed": "calico",
    "fluffiness": 6,
    "cuteness": 7
  },
  {
    "id": 2,
    "name": "Max",
    "breed": "unknown",
    "fluffiness": 5,
    "cuteness": 10
  }
]
```

This endpoint retrieves all kittens.

### HTTP Request

`GET http://example.com/api/kittens`

### Query Parameters

Parameter | Default | Description
--------- | ------- | -----------
include_cats | false | If set to true, the result will also include cats.
available | true | If set to false, the result will include kittens that have already been adopted.

<aside class="success">
Remember — a happy kitten is an authenticated kitten!
</aside>

## Get a Specific Kitten

```ruby
require 'kittn'

api = Kittn::APIClient.authorize!('meowmeowmeow')
api.kittens.get(2)
```

```python
import kittn

api = kittn.authorize('meowmeowmeow')
api.kittens.get(2)
```

```shell
curl "http://example.com/api/kittens/2"
  -H "Authorization: meowmeowmeow"
```

```javascript
const kittn = require('kittn');

let api = kittn.authorize('meowmeowmeow');
let max = api.kittens.get(2);
```

> The above command returns JSON structured like this:

```json
{
  "id": 2,
  "name": "Max",
  "breed": "unknown",
  "fluffiness": 5,
  "cuteness": 10
}
```

This endpoint retrieves a specific kitten.

<aside class="warning">Inside HTML code blocks like this one, you can't use Markdown, so use <code>&lt;code&gt;</code> blocks to denote code.</aside>

### HTTP Request

`GET http://example.com/kittens/<ID>`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the kitten to retrieve

