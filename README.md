# Basic認証
- ID: admin
- PW: Password

# データベース設計

# ER図
![人生を変えるフリマアプリ](https://user-images.githubusercontent.com/64017216/82408857-74527b80-9aa7-11ea-87cd-8e24afd002b1.png)

## itemsテーブル
|Column|Type|Options|
|------|----|-------|
|name|string|null: false, index: true|
|text|text|null: false|
|brand|string||
|status|integer|null:false, dafault: 0|
|delivery_charge_bearer|integer|null:false, dafault: 0|
|shipping_area|integer|null: false, dafault: 0|
|dalivery_days|integer|null:false, dafault: 0|
|price|integer|null:false|
|user_id|references|null: false, foreign_key: true|
|category_id|references|null: false, foreign_key: true|

### Association
- belongs_to :user
- belongs_to :category
- has_many :item_images, dependent: :destroy


## categoriesテーブル
|Column|Type|Options|
|------|----|-------|
|name|string|null: false|

### 指定gem
gem 'ancestry', '~> 1.2'
### Association
- has_many :items
- has_ancestry


## item_imagesテーブル
|Column|Type|Options|
|------|----|-------|
|src|string|null: false|
|item_id|references|null: false, foreign_key: true|

### Association
- belongs_to :item


## usersテーブル
|Column|Type|Options|
|------|----|-------|
|nickname|string|null: false|
|email|string|null: false, unique: true|
|password|string|null: false|

### Association
- has_one :profile, dependent: :destroy
- has_one :user_address, dependent: :destroy
- has_one :payment_card, dependent: :destroy
- has_many :items, dependent: :destroy


## profilesテーブル
|Column|Type|Options|
|------|----|-------|
|family_name|string|null: false|
|first_name|string|null:false|
|family_name_furigana|string|null:false|
|first_name_furigana|string|null: false|
|birth_year|integer|null:false, default: 0|
|birth_month|integer|null:false, default: 0|
|birth_date|integer|null:false, default: 0|
|user_id|references|null: false, foreign_key: true|

### Association
- belongs_to :user


## addressesテーブル
|Column|Type|Options|
|------|----|-------|
|family_name|string|null: false|
|first_name|string|null:false|
|family_name_kana|string|null:false|
|first_name_kana|string|null: false|
|post_number|integer|null:false|
|prefecture|integer|null:false, dafault: 0|
|city|string|null:false|
|house_number|integer|null: false|
|building_name|string||
|phone_number|integer||
|user_id|references|null: false, foreign_key: true|

### Association
- belongs_to :user

## payment_cardsテーブル
|Column|Type|Options|
|------|----|-------|
|user_id|references|null: false, foreign_key: true|
|customer_id|string|null:false|

### Association
- belongs_to :user