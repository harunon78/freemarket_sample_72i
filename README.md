# README

This README would normally document whatever steps are necessary to get the
application up and running.

Things you may want to cover:

* Ruby version

* System dependencies

* Configuration

* Database creation

* Database initialization

* How to run the test suite

* Services (job queues, cache servers, search engines, etc.)

* Deployment instructions

* ...

## テーブルの設計図
![フリマ ER 図](https://user-images.githubusercontent.com/61731113/78106702-de975a00-742e-11ea-83b5-b5058c17fd3b.jpeg)

## usersテーブル
|Column            |Type   |Option                  |
|------------------|-------|------------------------|
|first_name        |string |null: false             |
|last_name         |string |null: false             |
|email             |string |null: false, default: ""|
|encrypted_password|string |null: false, default: ""|
|first_name_kana   |string |null: false             |
|last_name_kana    |string |null: false             |
|nickname          |string |null: false             |
|iamge             |text   |                        |
|birthday_year     |integer|null: false             |
|birthday_manth    |integer|null: false             |
|birthday_day      |integer|null: false             |

### Association
- has_one  :card
- has_many :likes
- has_many :products
- has_many :addresses


## addressesテーブル
|Column            |Type       |Option                       |
|------------------|-----------|-----------------------------|
|first_name        |string     |null: false                  |
|last_name         |string     |null: false                  |
|first_name_kana   |string     |null: false                  |
|last_name_kana    |string     |null: false                  |
|postal_code       |integer    |null: false                  |
|prefectures       |string     |null: false                  |
|municipality      |string     |null: false                  |
|house_number      |string     |null: false                  |
|apartment_name    |string     |null: false                  |
|call_number       |integer    |null: false, unique: true    |
|user_id           |references |null: false, foreign_key:true|

### Association
- belongs_to :user
- belongs_to :product

## productsテーブル
|Column|Type|Option                |
|-----------|----------|-----------|
|name       |string    |null: false|
|price      |integer   |null: false|
|status     |integer   |null: false|
|description|text      |null: false|
|sending    |integer   |null: false|
|send_cost  |integer   |null: false|
|user_id    |references|null: false|
|category_id|references|null: false|
|brand_id   |references|null: false|


statusはenumで管理
Productモデルでbrand_new(新品), very_good(良), good(可)とした

### Association
- belongs_to :user
- belongs_to :category
- belongs_to :brand
- has_one    :address
- has_many   :likes
- has_many   :images


## categoriesテーブル
|Column    |Type  |Options|
|----------|------|-------|
|name      |string|       |
|ancestry  |string|       |


|Column         |Type  |Options|
|---------------|------|-------|
|category_name  |string|       |
|category_detail|string|       |

### Association
- has_many :products


## brandsテーブル

|Column    |Type  |Options|
|----------|------|-------|
|brand_name|string|       |

### Association
- has_many :products


## cardsテーブル

|Column        |Type     |Options                       |
|--------------|---------|------------------------------|
|user_id       |integer  |null: false                   |
|customer_id   |string   |null: false                   |
|card_id       |integer  |null: false                   |


### Association
- belongs_to :user


## imagesテーブル

|Column |Type      |Options                       |
|-------|----------|------------------------------|
|image  |text      |null: false                   |
|product|references|null: false, foreign_key: true|

### Association
- belongs_to :product

## likesテーブル

|Column    |Type      |Options                       |
|----------|----------|------------------------------|
|user_id   |references|null: false, foreign_key: true|
|product_id|references|null: false, foreign_key: true|

### Association
- belongs_to :user
- belongs_to :product

## sns_credentialsテーブル

|Column   |Type      |Options                       |
|---------|----------|------------------------------|
|provider |string    |null: false                   |
|uid      |string    |null: false                   |
|user_id  |references|null: false, foreign_key: true|

### Association
- belongs_to :user

## commentsテーブル

|Column     |Type     |Options                       |
|-----------|---------|------------------------------|
|user_id    |integer  |null: false, foreign_key: true|
|product_id |integer  |null: false, foreign_key: true|
|comment    |text     |null:false                    |

### Association
- berongs_to :user
- berongs_to :product
