#### 建表语句：

```
create database `store_backstage`

// 商户
create table `user`(
  `user_id` int(11) NOT NULL AUTO_INCREMENT,
  `username` varchar(20) NOT NULL DEFAULT '',
  `password` varchar(50) NOT NULL DEFAULT '',
  `last_visit` timestamp NOT NULL DEFAULT CURRENT_TIMESTAMP,
  `created_at` timestamp NOT NULL DEFAULT CURRENT_TIMESTAMP,
  `phone` varchar(50) NOT NULL DEFAULT '',
  PRIMARY KEY (`user_id`)
)ENGINE=InnoDB DEFAULT CHARSET=utf8

// 商铺
create table `store`(
  `store_id` int(11) NOT NULL AUTO_INCREMENT,
  `name` varchar(20) NOT NULL DEFAULT '',
  `logo` varchar(100) NOT NULL DEFAULT '',
  `address` varchar(100) NOT NULL DEFAULT '',
  `category` varchar(20) NOT NULL DEFAULT '',
  `description` varchar(255) NOT NULL DEFAULT '',
  `phone` varchar(20) NOT NULL DEFAULT '',
  `sale_from` varchar(20) NOT NULL DEFAULT '',
  `sale_to` varchar(20) NOT NULL DEFAULT '',
  `avg_price` varchar(10) NOT NULL DEFATLT '',
  `created_at` timestamp NOT NULL DEFAULT CURRENT_TIMESTAMP,
  `user_id` int(11),
  PRIMARY KEY (`store_id`),
  CONSTRAINT `store_user` FOREIGN KEY (`user_id`) REFERENCES `user` (`user_id`) ON DELETE CASCADE ON UPDATE CASCADE
)ENGINE=InnoDB DEFAULT CHARSET=utf8

// 分类
create table `category`(
  `cat_id` int(11) NOT NULL AUTO_INCREMENT,
  `name` varchar(20) NOT NULL DEFAULT '',
  `created_at` timestamp NOT NULL DEFAULT CURRENT_TIMESTAMP,
  `sequence` int(20) NOT NULL DEFAULT 0,
  `user_id` int(11),
  PRIMARY KEY (`cat_id`),
  CONSTRAINT `category_user` FOREIGN KEY (`user_id`) REFERENCES `user` (`user_id`) ON DELETE CASCADE ON UPDATE CASCADE
)ENGINE=InnoDB DEFAULT CHARSET=utf8

// 商品
create table `goods`(
  `goods_id` int(11) NOT NULL AUTO_INCREMENT,
  `name` varchar(20) NOT NULL DEFAULT '',
  `created_at` timestamp NOT NULL DEFAULT CURRENT_TIMESTAMP,
  `specification` varchar(30) NOT NULL DEFAULT 0,
  `picture` varchar(100) NOT NULL DEFAULT '',
  `price` decimal(10,2) NOT NULL DEFAULT 0,
  `cost` decimal(10,2) NOT NULL DEFAULT 0,
  `sale_volume` int(10) NOT NULL DEFAULT 0,
  `stock` int(10) NOT NULL DEFAULT 0,
  `on_sale` tinyint(1) NOT NULL DEFAULT 1,
  `user_id` int(11),
  `cat_id` int(11),
  PRIMARY KEY (`goods_id`),
  CONSTRAINT `goods_user` FOREIGN KEY (`user_id`) REFERENCES `user` (`user_id`) ON DELETE CASCADE ON UPDATE CASCADE,
  CONSTRAINT `goods_category` FOREIGN KEY (`cat_id`) REFERENCES `category` (`cat_id`) ON DELETE CASCADE ON UPDATE CASCADE
)ENGINE=InnoDB DEFAULT CHARSET=utf8

// 会员
create table `member`(
  `member_id` int(11) NOT NULL AUTO_INCREMENT,
  `nickname` varchar(20) NOT NULL DEFAULT '',
  `phone` varchar(20) NOT NULL DEFAULT '',
  `card_no` varchar(20) NOT NULL DEFAULT '',
  `created_at` timestamp NOT NULL DEFAULT CURRENT_TIMESTAMP,
  `gender` int(1) NOT NULL DEFAULT 1,
  `credit` int(11) NOT NULL DEFAULT 0,
  `order_count` int(11) NOT NULL DEFAULT 0,
  `user_id` int(11),
  PRIMARY KEY (`member_id`),
  CONSTRAINT `member_user` FOREIGN KEY (`user_id`) REFERENCES `user` (`user_id`) ON DELETE CASCADE ON UPDATE CASCADE
)ENGINE=InnoDB DEFAULT CHARSET=utf8


insert into member (nickname, phone, card_no, gender, user_id) values ('落英坠露', '18328738478', '4387298748598737480', 1, 1)

```