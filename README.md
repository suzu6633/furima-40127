# テーブル設計

## profiles テーブル

| Column             | Type       | Options                        |
| ------------------ | ---------- | ------------------------------ |
| introduction       | text       |                                |
| avatar             | string     |                                |
| user               | references | null: false, foreign_key: true |

### Association

 - belongs_to :user

## users テーブル

| Column            | Type       | Options                                |
| ----------------- | ---------- | -------------------------------------- |
| nickname          | string     | null: false                            |
| password          | string     | null: false                            |
| email             | string     | null: false, unique: true, index: true |
| first_name        | string     | null: false                            |
| family_name       | string     | null: false                            |
| first_name_kana   | string     | null: false                            |
| family_name_kana  | string     | null: false                            |
| post_code         | string     | null: false                            |
| city              | string     | null: false                            |
| house_number      | string     | null: false                            |
| building_name     | string     |                                        |
| phone_number      | string     | unique: true                           |
| birth_date        |            | date null: false                       |

### Association

 - has_many: seller_items, foreign_key: true
 - has_many: buyer_items, foreign_key: true
 - has_one: profile, dependent: :destroy
 - has_one: credit_card, dependent: :destroy


## credit_cards テーブル

| Column      | Type       | Options                        |
| ----------- | ---------- | ------------------------------ |
| user        | references | null: foreign_key: true        |
| customer_id | string     | null: false                    |
| card_id     | string     | null: false                    |

### Association

 - belongs_to :user

## items テーブル

| Column             | Type       | Options                   |
| ------------------ | ---------- | ------------------------- |
| name               | string     | null: false               |
| introduction       | text       | null: false               |
| price              | integer    | null: false               |
| brand              | integer    |                           |
| item_condition     | integer    | null: false               |
| postage_payer      | integer    | null: false               |
| preparation_day    | integer    | null: false               |
| postage_type       | integer    | null: false               |
| category           | integer    | null: false               |
| trading_status     | integer    | null: false               |
| seller             | references | null: false               |
| buyer              | references | null: false               |

### Association

 - has_many :item_images, dependent: :destroy
 - belongs_to :category
 - belongs_to_active_hash :item_condition
 - belongs_to_active_hash :preparation_day
 - belongs_to_active_hash :postage_type
 - belongs_to_active_hash :postage_payer
 - belongs_to :brand
 - belongs_to :seller, class_name: "User"
 - belongs_to :buyer, class_name: "User"


## items_images テーブル

| Column     | Type       | Options                        |
| ---------- | ---------- | ------------------------------ |
| url        | string     | null: false                    |
| item       | references | null: false                    |

### Association

 - belongs_to :item

## categories テーブル

| Column   | Type   | Options                   |
| ---------| ------ | ------------------------- |
| name     | string | null: false               |
| ancestor | string |                           |

### Association

 - has_many :items

## item_conditions (active_hash) テーブル

| Column         | Type       | Options                        |
| -------------- | ---------- | ------------------------------ |
| item_condition | integer    | null: false                    |

### Association

 - has_many :items

## preparation_days (active_hash) テーブル

| Column             | Type    | Options                   |
| ------------------ | ------- | ------------------------- |
| preparation_day    | integer | null: false               |

### Association

 - has_many :items

## postage_types (active_hash) テーブル

| Column       | Type       | Options                        |
| ------------ | ---------- | ------------------------------ |
| postage_type | integer    | null: false                    |

### Association

 - has_many :items

## postage_payers (active_hash) テーブル

| Column             | Type    | Options                   |
| ------------------ | ------- | ------------------------- |
| postage_payer      | integer | null: false               |

### Association

 - has_many :items

## brands (active_hash) テーブル

| Column     | Type       | Options                        |
| ---------- | ---------- | ------------------------------ |
| name       | string     |                                |

### Association

 - has_many :items