# Kakedashi DB設計
## usersテーブル
|Column|Type|Option|
|------|----|------|
|nickname|string|null: false|
|email|string|null: false, unique: true|
|password|string|null: false|
|image|string||
### Association
- has_many :posts, dependent: :destroy
- has_many :likes, dependent: :destroy
- has_many :liked_posts, through: :likes, source: :post
- has_many :comments

## postsテーブル
|Column|Type|Option|
|------|----|------|
|text|text|null: false|
|user|references|null: false, foreign_key: true|
### Association
- belongs_to :user dependent: :destroy
- has_many :likes
- has_many :liked_users, through: :likes, source: :user
- has_many :comments


## commentsテーブル
|Column|Type|Option|
|------|----|------|
|user_id|integer||
|post_id|integer||
|content|text||

### Association
- belongs_to :post
- belongs_to :user

## likessテーブル
|Column|Type|Option|
|------|----|------|
|post|references|null: false|
|user|references|null: false|

### Association
- belongs_to :user
- belongs_to :post 
