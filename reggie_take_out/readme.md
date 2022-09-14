技术栈-

`springboot`+`mybatisplus`+`Restful`



# 开发环境搭建

## 数据库环境搭建

```sql

SET FOREIGN_KEY_CHECKS=0;

DROP TABLE IF EXISTS `address_book`;
CREATE TABLE `address_book` (
  `id` bigint(20) NOT NULL COMMENT '主键',
  `user_id` bigint(20) NOT NULL COMMENT '用户id',
  `consignee` varchar(50) COLLATE utf8_bin NOT NULL COMMENT '收货人',
  `sex` tinyint(4) NOT NULL COMMENT '性别 0 女 1 男',
  `phone` varchar(11) COLLATE utf8_bin NOT NULL COMMENT '手机号',
  `province_code` varchar(12) CHARACTER SET utf8mb4 DEFAULT NULL COMMENT '省级区划编号',
  `province_name` varchar(32) CHARACTER SET utf8mb4 DEFAULT NULL COMMENT '省级名称',
  `city_code` varchar(12) CHARACTER SET utf8mb4 DEFAULT NULL COMMENT '市级区划编号',
  `city_name` varchar(32) CHARACTER SET utf8mb4 DEFAULT NULL COMMENT '市级名称',
  `district_code` varchar(12) CHARACTER SET utf8mb4 DEFAULT NULL COMMENT '区级区划编号',
  `district_name` varchar(32) CHARACTER SET utf8mb4 DEFAULT NULL COMMENT '区级名称',
  `detail` varchar(200) CHARACTER SET utf8mb4 DEFAULT NULL COMMENT '详细地址',
  `label` varchar(100) CHARACTER SET utf8mb4 DEFAULT NULL COMMENT '标签',
  `is_default` tinyint(1) NOT NULL DEFAULT '0' COMMENT '默认 0 否 1是',
  `create_time` datetime NOT NULL COMMENT '创建时间',
  `update_time` datetime NOT NULL COMMENT '更新时间',
  `create_user` bigint(20) NOT NULL COMMENT '创建人',
  `update_user` bigint(20) NOT NULL COMMENT '修改人',
  `is_deleted` int(11) NOT NULL DEFAULT '0' COMMENT '是否删除',
  PRIMARY KEY (`id`) USING BTREE
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COLLATE=utf8_bin COMMENT='地址管理';

-- ----------------------------
-- Records of address_book
-- ----------------------------
INSERT INTO `address_book` VALUES ('1417414526093082626', '1417012167126876162', '小明', '1', '13812345678', null, null, null, null, null, null, '昌平区金燕龙办公楼', '公司', '1', '2021-07-20 17:22:12', '2021-07-20 17:26:33', '1417012167126876162', '1417012167126876162', '0');
INSERT INTO `address_book` VALUES ('1417414926166769666', '1417012167126876162', '小李', '1', '13512345678', null, null, null, null, null, null, '测试', '家', '0', '2021-07-20 17:23:47', '2021-07-20 17:23:47', '1417012167126876162', '1417012167126876162', '0');

-- ----------------------------
-- Table structure for category
-- ----------------------------
DROP TABLE IF EXISTS `category`;
CREATE TABLE `category` (
  `id` bigint(20) NOT NULL COMMENT '主键',
  `type` int(11) DEFAULT NULL COMMENT '类型   1 菜品分类 2 套餐分类',
  `name` varchar(64) COLLATE utf8_bin NOT NULL COMMENT '分类名称',
  `sort` int(11) NOT NULL DEFAULT '0' COMMENT '顺序',
  `create_time` datetime NOT NULL COMMENT '创建时间',
  `update_time` datetime NOT NULL COMMENT '更新时间',
  `create_user` bigint(20) NOT NULL COMMENT '创建人',
  `update_user` bigint(20) NOT NULL COMMENT '修改人',
  PRIMARY KEY (`id`) USING BTREE,
  UNIQUE KEY `idx_category_name` (`name`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COLLATE=utf8_bin COMMENT='菜品及套餐分类';

-- ----------------------------
-- Records of category
-- ----------------------------
INSERT INTO `category` VALUES ('1397844263642378242', '1', '湘菜', '1', '2021-05-27 09:16:58', '2021-07-15 20:25:23', '1', '1');
INSERT INTO `category` VALUES ('1397844303408574465', '1', '川菜', '2', '2021-05-27 09:17:07', '2021-06-02 14:27:22', '1', '1');
INSERT INTO `category` VALUES ('1397844391040167938', '1', '粤菜', '3', '2021-05-27 09:17:28', '2021-07-09 14:37:13', '1', '1');
INSERT INTO `category` VALUES ('1413341197421846529', '1', '饮品', '11', '2021-07-09 11:36:15', '2021-07-09 14:39:15', '1', '1');
INSERT INTO `category` VALUES ('1413342269393674242', '2', '商务套餐', '5', '2021-07-09 11:40:30', '2021-07-09 14:43:45', '1', '1');
INSERT INTO `category` VALUES ('1413384954989060097', '1', '主食', '12', '2021-07-09 14:30:07', '2021-07-09 14:39:19', '1', '1');
INSERT INTO `category` VALUES ('1413386191767674881', '2', '儿童套餐', '6', '2021-07-09 14:35:02', '2021-07-09 14:39:05', '1', '1');

-- ----------------------------
-- Table structure for dish
-- ----------------------------
DROP TABLE IF EXISTS `dish`;
CREATE TABLE `dish` (
  `id` bigint(20) NOT NULL COMMENT '主键',
  `name` varchar(64) COLLATE utf8_bin NOT NULL COMMENT '菜品名称',
  `category_id` bigint(20) NOT NULL COMMENT '菜品分类id',
  `price` decimal(10,2) DEFAULT NULL COMMENT '菜品价格',
  `code` varchar(64) COLLATE utf8_bin NOT NULL COMMENT '商品码',
  `image` varchar(200) COLLATE utf8_bin NOT NULL COMMENT '图片',
  `description` varchar(400) COLLATE utf8_bin DEFAULT NULL COMMENT '描述信息',
  `status` int(11) NOT NULL DEFAULT '1' COMMENT '0 停售 1 起售',
  `sort` int(11) NOT NULL DEFAULT '0' COMMENT '顺序',
  `create_time` datetime NOT NULL COMMENT '创建时间',
  `update_time` datetime NOT NULL COMMENT '更新时间',
  `create_user` bigint(20) NOT NULL COMMENT '创建人',
  `update_user` bigint(20) NOT NULL COMMENT '修改人',
  `is_deleted` int(11) NOT NULL DEFAULT '0' COMMENT '是否删除',
  PRIMARY KEY (`id`) USING BTREE,
  UNIQUE KEY `idx_dish_name` (`name`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COLLATE=utf8_bin COMMENT='菜品管理';

-- ----------------------------
-- Records of dish
-- ----------------------------
INSERT INTO `dish` VALUES ('1397849739276890114', '辣子鸡', '1397844263642378242', '7800.00', '222222222', 'f966a38e-0780-40be-bb52-5699d13cb3d9.jpg', '来自鲜嫩美味的小鸡，值得一尝', '1', '0', '2021-05-27 09:38:43', '2021-05-27 09:38:43', '1', '1', '0');
INSERT INTO `dish` VALUES ('1397850140982161409', '毛氏红烧肉', '1397844263642378242', '6800.00', '123412341234', '0a3b3288-3446-4420-bbff-f263d0c02d8e.jpg', '毛氏红烧肉毛氏红烧肉，确定不来一份？', '1', '0', '2021-05-27 09:40:19', '2021-05-27 09:40:19', '1', '1', '0');
INSERT INTO `dish` VALUES ('1397850392090947585', '组庵鱼翅', '1397844263642378242', '4800.00', '123412341234', '740c79ce-af29-41b8-b78d-5f49c96e38c4.jpg', '组庵鱼翅，看图足以表明好吃程度', '1', '0', '2021-05-27 09:41:19', '2021-05-27 09:41:19', '1', '1', '0');
INSERT INTO `dish` VALUES ('1397850851245600769', '霸王别姬', '1397844263642378242', '12800.00', '123412341234', '057dd338-e487-4bbc-a74c-0384c44a9ca3.jpg', '还有什么比霸王别姬更美味的呢？', '1', '0', '2021-05-27 09:43:08', '2021-05-27 09:43:08', '1', '1', '0');
INSERT INTO `dish` VALUES ('1397851099502260226', '全家福', '1397844263642378242', '11800.00', '23412341234', 'a53a4e6a-3b83-4044-87f9-9d49b30a8fdc.jpg', '别光吃肉啦，来份全家福吧，让你长寿又美味', '1', '0', '2021-05-27 09:44:08', '2021-05-27 09:44:08', '1', '1', '0');
INSERT INTO `dish` VALUES ('1397851370462687234', '邵阳猪血丸子', '1397844263642378242', '13800.00', '1246812345678', '2a50628e-7758-4c51-9fbb-d37c61cdacad.jpg', '看，美味不？来嘛来嘛，这才是最爱吖', '1', '0', '2021-05-27 09:45:12', '2021-05-27 09:45:12', '1', '1', '0');
INSERT INTO `dish` VALUES ('1397851668262465537', '口味蛇', '1397844263642378242', '16800.00', '1234567812345678', '0f4bd884-dc9c-4cf9-b59e-7d5958fec3dd.jpg', '爬行界的扛把子，东兴-口味蛇，让你欲罢不能', '1', '0', '2021-05-27 09:46:23', '2021-05-27 09:46:23', '1', '1', '0');
INSERT INTO `dish` VALUES ('1397852391150759938', '辣子鸡丁', '1397844303408574465', '8800.00', '2346812468', 'ef2b73f2-75d1-4d3a-beea-22da0e1421bd.jpg', '辣子鸡丁，辣子鸡丁，永远的魂', '1', '0', '2021-05-27 09:49:16', '2021-05-27 09:49:16', '1', '1', '0');
INSERT INTO `dish` VALUES ('1397853183287013378', '麻辣兔头', '1397844303408574465', '19800.00', '123456787654321', '2a2e9d66-b41d-4645-87bd-95f2cfeed218.jpg', '麻辣兔头的详细制作，麻辣鲜香，色泽红润，回味悠长', '1', '0', '2021-05-27 09:52:24', '2021-05-27 09:52:24', '1', '1', '0');
INSERT INTO `dish` VALUES ('1397853709101740034', '蒜泥白肉', '1397844303408574465', '9800.00', '1234321234321', 'd2f61d70-ac85-4529-9b74-6d9a2255c6d7.jpg', '多么的有食欲啊', '1', '0', '2021-05-27 09:54:30', '2021-05-27 09:54:30', '1', '1', '0');
INSERT INTO `dish` VALUES ('1397853890262118402', '鱼香肉丝', '1397844303408574465', '3800.00', '1234212321234', '8dcfda14-5712-4d28-82f7-ae905b3c2308.jpg', '鱼香肉丝简直就是我们童年回忆的一道经典菜，上学的时候点个鱼香肉丝盖饭坐在宿舍床上看着肥皂剧，绝了！现在完美复刻一下上学的时候感觉', '1', '0', '2021-05-27 09:55:13', '2021-05-27 09:55:13', '1', '1', '0');
INSERT INTO `dish` VALUES ('1397854652581064706', '麻辣水煮鱼', '1397844303408574465', '14800.00', '2345312·345321', '1fdbfbf3-1d86-4b29-a3fc-46345852f2f8.jpg', '鱼片是买的切好的鱼片，放几个虾，增加味道', '1', '0', '2021-05-27 09:58:15', '2021-05-27 09:58:15', '1', '1', '0');
INSERT INTO `dish` VALUES ('1397854865672679425', '鱼香炒鸡蛋', '1397844303408574465', '2000.00', '23456431·23456', '0f252364-a561-4e8d-8065-9a6797a6b1d3.jpg', '鱼香菜也是川味的特色。里面没有鱼却鱼香味', '1', '0', '2021-05-27 09:59:06', '2021-05-27 09:59:06', '1', '1', '0');
INSERT INTO `dish` VALUES ('1397860242057375745', '脆皮烧鹅', '1397844391040167938', '12800.00', '123456786543213456', 'e476f679-5c15-436b-87fa-8c4e9644bf33.jpeg', '“广东烤鸭美而香，却胜烧鹅说古冈（今新会），燕瘦环肥各佳妙，君休偏重便宜坊”，可见烧鹅与烧鸭在粤菜之中已早负盛名。作为广州最普遍和最受欢迎的烧烤肉食，以它的“色泽金红，皮脆肉嫩，味香可口”的特色，在省城各大街小巷的烧卤店随处可见。', '1', '0', '2021-05-27 10:20:27', '2021-05-27 10:20:27', '1', '1', '0');
INSERT INTO `dish` VALUES ('1397860578738352129', '白切鸡', '1397844391040167938', '6600.00', '12345678654', '9ec6fc2d-50d2-422e-b954-de87dcd04198.jpeg', '白切鸡是一道色香味俱全的特色传统名肴，又叫白斩鸡，是粤菜系鸡肴中的一种，始于清代的民间。白切鸡通常选用细骨农家鸡与沙姜、蒜茸等食材，慢火煮浸白切鸡皮爽肉滑，清淡鲜美。著名的泮溪酒家白切鸡，曾获商业部优质产品金鼎奖。湛江白切鸡更是驰名粤港澳。粤菜厨坛中，鸡的菜式有200余款之多，而最为人常食不厌的正是白切鸡，深受食家青睐。', '1', '0', '2021-05-27 10:21:48', '2021-05-27 10:21:48', '1', '1', '0');
INSERT INTO `dish` VALUES ('1397860792492666881', '烤乳猪', '1397844391040167938', '38800.00', '213456432123456', '2e96a7e3-affb-438e-b7c3-e1430df425c9.jpeg', '广式烧乳猪主料是小乳猪，辅料是蒜，调料是五香粉、芝麻酱、八角粉等，本菜品主要通过将食材放入炭火中烧烤而成。烤乳猪是广州最著名的特色菜，并且是“满汉全席”中的主打菜肴之一。烤乳猪也是许多年来广东人祭祖的祭品之一，是家家都少不了的应节之物，用乳猪祭完先人后，亲戚们再聚餐食用。', '1', '0', '2021-05-27 10:22:39', '2021-05-27 10:22:39', '1', '1', '0');
INSERT INTO `dish` VALUES ('1397860963880316929', '脆皮乳鸽', '1397844391040167938', '10800.00', '1234563212345', '3fabb83a-1c09-4fd9-892b-4ef7457daafa.jpeg', '“脆皮乳鸽”是广东菜中的一道传统名菜，属于粤菜系，具有皮脆肉嫩、色泽红亮、鲜香味美的特点，常吃可使身体强健，清肺顺气。随着菜品制作工艺的不断发展，逐渐形成了熟炸法、生炸法和烤制法三种制作方法。无论那种制作方法，都是在鸽子经过一系列的加工，挂脆皮水后再加工而成，正宗的“脆皮乳鸽皮脆肉嫩、色泽红亮、鲜香味美、香气馥郁。这三种方法的制作过程都不算复杂，但想达到理想的效果并不容易。', '1', '0', '2021-05-27 10:23:19', '2021-05-27 10:23:19', '1', '1', '0');
INSERT INTO `dish` VALUES ('1397861683434139649', '清蒸河鲜海鲜', '1397844391040167938', '38800.00', '1234567876543213456', '1405081e-f545-42e1-86a2-f7559ae2e276.jpeg', '新鲜的海鲜，清蒸是最好的处理方式。鲜，体会为什么叫海鲜。清蒸是广州最经典的烹饪手法，过去岭南地区由于峻山大岭阻隔，交通不便，经济发展起步慢，自家打的鱼放在锅里煮了就吃，没有太多的讲究，但却发现这清淡的煮法能使鱼的鲜甜跃然舌尖。', '1', '0', '2021-05-27 10:26:11', '2021-05-27 10:26:11', '1', '1', '0');
INSERT INTO `dish` VALUES ('1397862198033297410', '老火靓汤', '1397844391040167938', '49800.00', '123456786532455', '583df4b7-a159-4cfc-9543-4f666120b25f.jpeg', '老火靓汤又称广府汤，是广府人传承数千年的食补养生秘方，慢火煲煮的中华老火靓汤，火候足，时间长，既取药补之效，又取入口之甘甜。 广府老火汤种类繁多，可以用各种汤料和烹调方法，烹制出各种不同口味、不同功效的汤来。', '1', '0', '2021-05-27 10:28:14', '2021-05-27 10:28:14', '1', '1', '0');
INSERT INTO `dish` VALUES ('1397862477831122945', '上汤焗龙虾', '1397844391040167938', '108800.00', '1234567865432', '5b8d2da3-3744-4bb3-acdc-329056b8259d.jpeg', '上汤焗龙虾是一道色香味俱全的传统名菜，属于粤菜系。此菜以龙虾为主料，配以高汤制成的一道海鲜美食。本品肉质洁白细嫩，味道鲜美，蛋白质含量高，脂肪含量低，营养丰富。是色香味俱全的传统名菜。', '1', '0', '2021-05-27 10:29:20', '2021-05-27 10:29:20', '1', '1', '0');
INSERT INTO `dish` VALUES ('1413342036832100354', '北冰洋', '1413341197421846529', '500.00', '', 'c99e0aab-3cb7-4eaa-80fd-f47d4ffea694.png', '', '1', '0', '2021-07-09 11:39:35', '2021-07-09 15:12:18', '1', '1', '0');
INSERT INTO `dish` VALUES ('1413384757047271425', '王老吉', '1413341197421846529', '500.00', '', '00874a5e-0df2-446b-8f69-a30eb7d88ee8.png', '', '1', '0', '2021-07-09 14:29:20', '2021-07-12 09:09:16', '1', '1', '0');
INSERT INTO `dish` VALUES ('1413385247889891330', '米饭', '1413384954989060097', '200.00', '', 'ee04a05a-1230-46b6-8ad5-1a95b140fff3.png', '', '1', '0', '2021-07-09 14:31:17', '2021-07-11 16:35:26', '1', '1', '0');

-- ----------------------------
-- Table structure for dish_flavor
-- ----------------------------
DROP TABLE IF EXISTS `dish_flavor`;
CREATE TABLE `dish_flavor` (
  `id` bigint(20) NOT NULL COMMENT '主键',
  `dish_id` bigint(20) NOT NULL COMMENT '菜品',
  `name` varchar(64) COLLATE utf8_bin NOT NULL COMMENT '口味名称',
  `value` varchar(500) COLLATE utf8_bin DEFAULT NULL COMMENT '口味数据list',
  `create_time` datetime NOT NULL COMMENT '创建时间',
  `update_time` datetime NOT NULL COMMENT '更新时间',
  `create_user` bigint(20) NOT NULL COMMENT '创建人',
  `update_user` bigint(20) NOT NULL COMMENT '修改人',
  `is_deleted` int(11) NOT NULL DEFAULT '0' COMMENT '是否删除',
  PRIMARY KEY (`id`) USING BTREE
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COLLATE=utf8_bin COMMENT='菜品口味关系表';

-- ----------------------------
-- Records of dish_flavor
-- ----------------------------
INSERT INTO `dish_flavor` VALUES ('1397849417888346113', '1397849417854791681', '辣度', '[\"不辣\",\"微辣\",\"中辣\",\"重辣\"]', '2021-05-27 09:37:27', '2021-05-27 09:37:27', '1', '1', '0');
INSERT INTO `dish_flavor` VALUES ('1397849739297861633', '1397849739276890114', '忌口', '[\"不要葱\",\"不要蒜\",\"不要香菜\",\"不要辣\"]', '2021-05-27 09:38:43', '2021-05-27 09:38:43', '1', '1', '0');
INSERT INTO `dish_flavor` VALUES ('1397849739323027458', '1397849739276890114', '辣度', '[\"不辣\",\"微辣\",\"中辣\",\"重辣\"]', '2021-05-27 09:38:43', '2021-05-27 09:38:43', '1', '1', '0');
INSERT INTO `dish_flavor` VALUES ('1397849936421761025', '1397849936404983809', '忌口', '[\"不要葱\",\"不要蒜\",\"不要香菜\",\"不要辣\"]', '2021-05-27 09:39:30', '2021-05-27 09:39:30', '1', '1', '0');
INSERT INTO `dish_flavor` VALUES ('1397849936438538241', '1397849936404983809', '辣度', '[\"不辣\",\"微辣\",\"中辣\",\"重辣\"]', '2021-05-27 09:39:30', '2021-05-27 09:39:30', '1', '1', '0');
INSERT INTO `dish_flavor` VALUES ('1397850141015715841', '1397850140982161409', '忌口', '[\"不要葱\",\"不要蒜\",\"不要香菜\",\"不要辣\"]', '2021-05-27 09:40:19', '2021-05-27 09:40:19', '1', '1', '0');
INSERT INTO `dish_flavor` VALUES ('1397850141040881665', '1397850140982161409', '辣度', '[\"不辣\",\"微辣\",\"中辣\",\"重辣\"]', '2021-05-27 09:40:19', '2021-05-27 09:40:19', '1', '1', '0');
INSERT INTO `dish_flavor` VALUES ('1397850392120307713', '1397850392090947585', '辣度', '[\"不辣\",\"微辣\",\"中辣\",\"重辣\"]', '2021-05-27 09:41:19', '2021-05-27 09:41:19', '1', '1', '0');
INSERT INTO `dish_flavor` VALUES ('1397850392137084929', '1397850392090947585', '辣度', '[\"不辣\",\"微辣\",\"中辣\",\"重辣\"]', '2021-05-27 09:41:19', '2021-05-27 09:41:19', '1', '1', '0');
INSERT INTO `dish_flavor` VALUES ('1397850630734262274', '1397850630700707841', '忌口', '[\"不要葱\",\"不要蒜\",\"不要香菜\",\"不要辣\"]', '2021-05-27 09:42:16', '2021-05-27 09:42:16', '1', '1', '0');
INSERT INTO `dish_flavor` VALUES ('1397850630755233794', '1397850630700707841', '辣度', '[\"微辣\",\"中辣\",\"重辣\"]', '2021-05-27 09:42:16', '2021-05-27 09:42:16', '1', '1', '0');
INSERT INTO `dish_flavor` VALUES ('1397850851274960898', '1397850851245600769', '忌口', '[\"不要蒜\",\"不要香菜\",\"不要辣\"]', '2021-05-27 09:43:08', '2021-05-27 09:43:08', '1', '1', '0');
INSERT INTO `dish_flavor` VALUES ('1397850851283349505', '1397850851245600769', '辣度', '[\"不辣\",\"微辣\",\"中辣\",\"重辣\"]', '2021-05-27 09:43:08', '2021-05-27 09:43:08', '1', '1', '0');
INSERT INTO `dish_flavor` VALUES ('1397851099523231745', '1397851099502260226', '忌口', '[\"不要葱\",\"不要蒜\",\"不要香菜\",\"不要辣\"]', '2021-05-27 09:44:08', '2021-05-27 09:44:08', '1', '1', '0');
INSERT INTO `dish_flavor` VALUES ('1397851099527426050', '1397851099502260226', '辣度', '[\"不辣\",\"微辣\",\"中辣\"]', '2021-05-27 09:44:08', '2021-05-27 09:44:08', '1', '1', '0');
INSERT INTO `dish_flavor` VALUES ('1397851370483658754', '1397851370462687234', '温度', '[\"热饮\",\"常温\",\"去冰\",\"少冰\",\"多冰\"]', '2021-05-27 09:45:12', '2021-05-27 09:45:12', '1', '1', '0');
INSERT INTO `dish_flavor` VALUES ('1397851370483658755', '1397851370462687234', '忌口', '[\"不要葱\",\"不要蒜\",\"不要香菜\",\"不要辣\"]', '2021-05-27 09:45:12', '2021-05-27 09:45:12', '1', '1', '0');
INSERT INTO `dish_flavor` VALUES ('1397851370483658756', '1397851370462687234', '辣度', '[\"不辣\",\"微辣\",\"中辣\",\"重辣\"]', '2021-05-27 09:45:12', '2021-05-27 09:45:12', '1', '1', '0');
INSERT INTO `dish_flavor` VALUES ('1397851668283437058', '1397851668262465537', '温度', '[\"热饮\",\"常温\",\"去冰\",\"少冰\",\"多冰\"]', '2021-05-27 09:46:23', '2021-05-27 09:46:23', '1', '1', '0');
INSERT INTO `dish_flavor` VALUES ('1397852391180120065', '1397852391150759938', '忌口', '[\"不要葱\",\"不要香菜\",\"不要辣\"]', '2021-05-27 09:49:16', '2021-05-27 09:49:16', '1', '1', '0');
INSERT INTO `dish_flavor` VALUES ('1397852391196897281', '1397852391150759938', '辣度', '[\"不辣\",\"微辣\",\"重辣\"]', '2021-05-27 09:49:16', '2021-05-27 09:49:16', '1', '1', '0');
INSERT INTO `dish_flavor` VALUES ('1397853183307984898', '1397853183287013378', '辣度', '[\"不辣\",\"微辣\",\"中辣\",\"重辣\"]', '2021-05-27 09:52:24', '2021-05-27 09:52:24', '1', '1', '0');
INSERT INTO `dish_flavor` VALUES ('1397853423486414850', '1397853423461249026', '辣度', '[\"不辣\",\"微辣\",\"中辣\",\"重辣\"]', '2021-05-27 09:53:22', '2021-05-27 09:53:22', '1', '1', '0');
INSERT INTO `dish_flavor` VALUES ('1397853709126905857', '1397853709101740034', '忌口', '[\"不要葱\",\"不要蒜\",\"不要香菜\",\"不要辣\"]', '2021-05-27 09:54:30', '2021-05-27 09:54:30', '1', '1', '0');
INSERT INTO `dish_flavor` VALUES ('1397853890283089922', '1397853890262118402', '辣度', '[\"不辣\",\"微辣\",\"中辣\",\"重辣\"]', '2021-05-27 09:55:13', '2021-05-27 09:55:13', '1', '1', '0');
INSERT INTO `dish_flavor` VALUES ('1397854133632413697', '1397854133603053569', '温度', '[\"热饮\",\"常温\",\"去冰\",\"少冰\",\"多冰\"]', '2021-05-27 09:56:11', '2021-05-27 09:56:11', '1', '1', '0');
INSERT INTO `dish_flavor` VALUES ('1397854652623007745', '1397854652581064706', '忌口', '[\"不要葱\",\"不要蒜\",\"不要香菜\",\"不要辣\"]', '2021-05-27 09:58:15', '2021-05-27 09:58:15', '1', '1', '0');
INSERT INTO `dish_flavor` VALUES ('1397854652635590658', '1397854652581064706', '辣度', '[\"不辣\",\"微辣\",\"中辣\",\"重辣\"]', '2021-05-27 09:58:15', '2021-05-27 09:58:15', '1', '1', '0');
INSERT INTO `dish_flavor` VALUES ('1397854865735593986', '1397854865672679425', '辣度', '[\"不辣\",\"微辣\",\"中辣\",\"重辣\"]', '2021-05-27 09:59:06', '2021-05-27 09:59:06', '1', '1', '0');
INSERT INTO `dish_flavor` VALUES ('1397855742303186946', '1397855742273826817', '辣度', '[\"不辣\",\"微辣\",\"中辣\",\"重辣\"]', '2021-05-27 10:02:35', '2021-05-27 10:02:35', '1', '1', '0');
INSERT INTO `dish_flavor` VALUES ('1397855906497605633', '1397855906468245506', '忌口', '[\"不要葱\",\"不要蒜\",\"不要香菜\",\"不要辣\"]', '2021-05-27 10:03:14', '2021-05-27 10:03:14', '1', '1', '0');
INSERT INTO `dish_flavor` VALUES ('1397856190573621250', '1397856190540066818', '辣度', '[\"不辣\",\"微辣\",\"中辣\",\"重辣\"]', '2021-05-27 10:04:21', '2021-05-27 10:04:21', '1', '1', '0');
INSERT INTO `dish_flavor` VALUES ('1397859056709316609', '1397859056684150785', '辣度', '[\"不辣\",\"微辣\",\"中辣\",\"重辣\"]', '2021-05-27 10:15:45', '2021-05-27 10:15:45', '1', '1', '0');
INSERT INTO `dish_flavor` VALUES ('1397859277837217794', '1397859277812051969', '辣度', '[\"不辣\",\"微辣\",\"中辣\",\"重辣\"]', '2021-05-27 10:16:37', '2021-05-27 10:16:37', '1', '1', '0');
INSERT INTO `dish_flavor` VALUES ('1397859487502086146', '1397859487476920321', '辣度', '[\"不辣\",\"微辣\",\"中辣\",\"重辣\"]', '2021-05-27 10:17:27', '2021-05-27 10:17:27', '1', '1', '0');
INSERT INTO `dish_flavor` VALUES ('1397859757061615618', '1397859757036449794', '甜味', '[\"无糖\",\"少糖\",\"半躺\",\"多糖\",\"全糖\"]', '2021-05-27 10:18:32', '2021-05-27 10:18:32', '1', '1', '0');
INSERT INTO `dish_flavor` VALUES ('1397860242086735874', '1397860242057375745', '辣度', '[\"不辣\",\"微辣\",\"中辣\",\"重辣\"]', '2021-05-27 10:20:27', '2021-05-27 10:20:27', '1', '1', '0');
INSERT INTO `dish_flavor` VALUES ('1397860963918065665', '1397860963880316929', '辣度', '[\"不辣\",\"微辣\",\"中辣\",\"重辣\"]', '2021-05-27 10:23:19', '2021-05-27 10:23:19', '1', '1', '0');
INSERT INTO `dish_flavor` VALUES ('1397861135754506242', '1397861135733534722', '甜味', '[\"无糖\",\"少糖\",\"半躺\",\"多糖\",\"全糖\"]', '2021-05-27 10:24:00', '2021-05-27 10:24:00', '1', '1', '0');
INSERT INTO `dish_flavor` VALUES ('1397861370035744769', '1397861370010578945', '辣度', '[\"不辣\",\"微辣\",\"中辣\",\"重辣\"]', '2021-05-27 10:24:56', '2021-05-27 10:24:56', '1', '1', '0');
INSERT INTO `dish_flavor` VALUES ('1397861683459305474', '1397861683434139649', '忌口', '[\"不要葱\",\"不要蒜\",\"不要香菜\",\"不要辣\"]', '2021-05-27 10:26:11', '2021-05-27 10:26:11', '1', '1', '0');
INSERT INTO `dish_flavor` VALUES ('1397861898467717121', '1397861898438356993', '忌口', '[\"不要葱\",\"不要蒜\",\"不要香菜\",\"不要辣\"]', '2021-05-27 10:27:02', '2021-05-27 10:27:02', '1', '1', '0');
INSERT INTO `dish_flavor` VALUES ('1397862198054268929', '1397862198033297410', '忌口', '[\"不要葱\",\"不要蒜\",\"不要香菜\",\"不要辣\"]', '2021-05-27 10:28:14', '2021-05-27 10:28:14', '1', '1', '0');
INSERT INTO `dish_flavor` VALUES ('1397862477835317250', '1397862477831122945', '辣度', '[\"不辣\",\"微辣\",\"中辣\"]', '2021-05-27 10:29:20', '2021-05-27 10:29:20', '1', '1', '0');
INSERT INTO `dish_flavor` VALUES ('1398089545865015297', '1398089545676271617', '温度', '[\"热饮\",\"常温\",\"去冰\",\"少冰\",\"多冰\"]', '2021-05-28 01:31:38', '2021-05-28 01:31:38', '1', '1', '0');
INSERT INTO `dish_flavor` VALUES ('1398089782323097601', '1398089782285348866', '辣度', '[\"不辣\",\"微辣\",\"中辣\",\"重辣\"]', '2021-05-28 01:32:34', '2021-05-28 01:32:34', '1', '1', '0');
INSERT INTO `dish_flavor` VALUES ('1398090003262255106', '1398090003228700673', '忌口', '[\"不要葱\",\"不要蒜\",\"不要香菜\",\"不要辣\"]', '2021-05-28 01:33:27', '2021-05-28 01:33:27', '1', '1', '0');
INSERT INTO `dish_flavor` VALUES ('1398090264554811394', '1398090264517062657', '忌口', '[\"不要葱\",\"不要蒜\",\"不要香菜\",\"不要辣\"]', '2021-05-28 01:34:29', '2021-05-28 01:34:29', '1', '1', '0');
INSERT INTO `dish_flavor` VALUES ('1398090455399837698', '1398090455324340225', '辣度', '[\"不辣\",\"微辣\",\"中辣\",\"重辣\"]', '2021-05-28 01:35:14', '2021-05-28 01:35:14', '1', '1', '0');
INSERT INTO `dish_flavor` VALUES ('1398090685449023490', '1398090685419663362', '温度', '[\"热饮\",\"常温\",\"去冰\",\"少冰\",\"多冰\"]', '2021-05-28 01:36:09', '2021-05-28 01:36:09', '1', '1', '0');
INSERT INTO `dish_flavor` VALUES ('1398090825358422017', '1398090825329061889', '忌口', '[\"不要葱\",\"不要蒜\",\"不要香菜\",\"不要辣\"]', '2021-05-28 01:36:43', '2021-05-28 01:36:43', '1', '1', '0');
INSERT INTO `dish_flavor` VALUES ('1398091007051476993', '1398091007017922561', '辣度', '[\"不辣\",\"微辣\",\"中辣\",\"重辣\"]', '2021-05-28 01:37:26', '2021-05-28 01:37:26', '1', '1', '0');
INSERT INTO `dish_flavor` VALUES ('1398091296164851713', '1398091296131297281', '辣度', '[\"不辣\",\"微辣\",\"中辣\",\"重辣\"]', '2021-05-28 01:38:35', '2021-05-28 01:38:35', '1', '1', '0');
INSERT INTO `dish_flavor` VALUES ('1398091546531246081', '1398091546480914433', '忌口', '[\"不要葱\",\"不要蒜\",\"不要香菜\",\"不要辣\"]', '2021-05-28 01:39:35', '2021-05-28 01:39:35', '1', '1', '0');
INSERT INTO `dish_flavor` VALUES ('1398091729809747969', '1398091729788776450', '辣度', '[\"不辣\",\"微辣\",\"中辣\",\"重辣\"]', '2021-05-28 01:40:18', '2021-05-28 01:40:18', '1', '1', '0');
INSERT INTO `dish_flavor` VALUES ('1398091889499484161', '1398091889449152513', '辣度', '[\"不辣\",\"微辣\",\"中辣\",\"重辣\"]', '2021-05-28 01:40:56', '2021-05-28 01:40:56', '1', '1', '0');
INSERT INTO `dish_flavor` VALUES ('1398092095179763713', '1398092095142014978', '辣度', '[\"不辣\",\"微辣\",\"中辣\",\"重辣\"]', '2021-05-28 01:41:45', '2021-05-28 01:41:45', '1', '1', '0');
INSERT INTO `dish_flavor` VALUES ('1398092283877306370', '1398092283847946241', '辣度', '[\"不辣\",\"微辣\",\"中辣\",\"重辣\"]', '2021-05-28 01:42:30', '2021-05-28 01:42:30', '1', '1', '0');
INSERT INTO `dish_flavor` VALUES ('1398094018939236354', '1398094018893099009', '辣度', '[\"不辣\",\"微辣\",\"中辣\",\"重辣\"]', '2021-05-28 01:49:24', '2021-05-28 01:49:24', '1', '1', '0');
INSERT INTO `dish_flavor` VALUES ('1398094391494094850', '1398094391456346113', '辣度', '[\"不辣\",\"微辣\",\"中辣\",\"重辣\"]', '2021-05-28 01:50:53', '2021-05-28 01:50:53', '1', '1', '0');
INSERT INTO `dish_flavor` VALUES ('1399574026165727233', '1399305325713600514', '辣度', '[\"不辣\",\"微辣\",\"中辣\",\"重辣\"]', '2021-06-01 03:50:25', '2021-06-01 03:50:25', '1399309715396669441', '1399309715396669441', '0');
INSERT INTO `dish_flavor` VALUES ('1413389540592263169', '1413384757047271425', '温度', '[\"常温\",\"冷藏\"]', '2021-07-12 09:09:16', '2021-07-12 09:09:16', '1', '1', '0');
INSERT INTO `dish_flavor` VALUES ('1413389684020682754', '1413342036832100354', '温度', '[\"常温\",\"冷藏\"]', '2021-07-09 15:12:18', '2021-07-09 15:12:18', '1', '1', '0');

-- ----------------------------
-- Table structure for employee
-- ----------------------------
DROP TABLE IF EXISTS `employee`;
CREATE TABLE `employee` (
  `id` bigint(20) NOT NULL COMMENT '主键',
  `name` varchar(32) COLLATE utf8_bin NOT NULL COMMENT '姓名',
  `username` varchar(32) COLLATE utf8_bin NOT NULL COMMENT '用户名',
  `password` varchar(64) COLLATE utf8_bin NOT NULL COMMENT '密码',
  `phone` varchar(11) COLLATE utf8_bin NOT NULL COMMENT '手机号',
  `sex` varchar(2) COLLATE utf8_bin NOT NULL COMMENT '性别',
  `id_number` varchar(18) COLLATE utf8_bin NOT NULL COMMENT '身份证号',
  `status` int(11) NOT NULL DEFAULT '1' COMMENT '状态 0:禁用，1:正常',
  `create_time` datetime NOT NULL COMMENT '创建时间',
  `update_time` datetime NOT NULL COMMENT '更新时间',
  `create_user` bigint(20) NOT NULL COMMENT '创建人',
  `update_user` bigint(20) NOT NULL COMMENT '修改人',
  PRIMARY KEY (`id`) USING BTREE,
  UNIQUE KEY `idx_username` (`username`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COLLATE=utf8_bin COMMENT='员工信息';

-- ----------------------------
-- Records of employee
-- ----------------------------
INSERT INTO `employee` VALUES ('1', '管理员', 'admin', 'e10adc3949ba59abbe56e057f20f883e', '13812312312', '1', '110101199001010047', '1', '2021-05-06 17:20:07', '2021-05-10 02:24:09', '1', '1');

-- ----------------------------
-- Table structure for orders
-- ----------------------------
DROP TABLE IF EXISTS `orders`;
CREATE TABLE `orders` (
  `id` bigint(20) NOT NULL COMMENT '主键',
  `number` varchar(50) COLLATE utf8_bin DEFAULT NULL COMMENT '订单号',
  `status` int(11) NOT NULL DEFAULT '1' COMMENT '订单状态 1待付款，2待派送，3已派送，4已完成，5已取消',
  `user_id` bigint(20) NOT NULL COMMENT '下单用户',
  `address_book_id` bigint(20) NOT NULL COMMENT '地址id',
  `order_time` datetime NOT NULL COMMENT '下单时间',
  `checkout_time` datetime NOT NULL COMMENT '结账时间',
  `pay_method` int(11) NOT NULL DEFAULT '1' COMMENT '支付方式 1微信,2支付宝',
  `amount` decimal(10,2) NOT NULL COMMENT '实收金额',
  `remark` varchar(100) COLLATE utf8_bin DEFAULT NULL COMMENT '备注',
  `phone` varchar(255) COLLATE utf8_bin DEFAULT NULL,
  `address` varchar(255) COLLATE utf8_bin DEFAULT NULL,
  `user_name` varchar(255) COLLATE utf8_bin DEFAULT NULL,
  `consignee` varchar(255) COLLATE utf8_bin DEFAULT NULL,
  PRIMARY KEY (`id`) USING BTREE
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COLLATE=utf8_bin COMMENT='订单表';

-- ----------------------------
-- Records of orders
-- ----------------------------

-- ----------------------------
-- Table structure for order_detail
-- ----------------------------
DROP TABLE IF EXISTS `order_detail`;
CREATE TABLE `order_detail` (
  `id` bigint(20) NOT NULL COMMENT '主键',
  `name` varchar(50) COLLATE utf8_bin DEFAULT NULL COMMENT '名字',
  `image` varchar(100) COLLATE utf8_bin DEFAULT NULL COMMENT '图片',
  `order_id` bigint(20) NOT NULL COMMENT '订单id',
  `dish_id` bigint(20) DEFAULT NULL COMMENT '菜品id',
  `setmeal_id` bigint(20) DEFAULT NULL COMMENT '套餐id',
  `dish_flavor` varchar(50) COLLATE utf8_bin DEFAULT NULL COMMENT '口味',
  `number` int(11) NOT NULL DEFAULT '1' COMMENT '数量',
  `amount` decimal(10,2) NOT NULL COMMENT '金额',
  PRIMARY KEY (`id`) USING BTREE
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COLLATE=utf8_bin COMMENT='订单明细表';

-- ----------------------------
-- Records of order_detail
-- ----------------------------

-- ----------------------------
-- Table structure for setmeal
-- ----------------------------
DROP TABLE IF EXISTS `setmeal`;
CREATE TABLE `setmeal` (
  `id` bigint(20) NOT NULL COMMENT '主键',
  `category_id` bigint(20) NOT NULL COMMENT '菜品分类id',
  `name` varchar(64) COLLATE utf8_bin NOT NULL COMMENT '套餐名称',
  `price` decimal(10,2) NOT NULL COMMENT '套餐价格',
  `status` int(11) DEFAULT NULL COMMENT '状态 0:停用 1:启用',
  `code` varchar(32) COLLATE utf8_bin DEFAULT NULL COMMENT '编码',
  `description` varchar(512) COLLATE utf8_bin DEFAULT NULL COMMENT '描述信息',
  `image` varchar(255) COLLATE utf8_bin DEFAULT NULL COMMENT '图片',
  `create_time` datetime NOT NULL COMMENT '创建时间',
  `update_time` datetime NOT NULL COMMENT '更新时间',
  `create_user` bigint(20) NOT NULL COMMENT '创建人',
  `update_user` bigint(20) NOT NULL COMMENT '修改人',
  `is_deleted` int(11) NOT NULL DEFAULT '0' COMMENT '是否删除',
  PRIMARY KEY (`id`) USING BTREE,
  UNIQUE KEY `idx_setmeal_name` (`name`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COLLATE=utf8_bin COMMENT='套餐';

-- ----------------------------
-- Records of setmeal
-- ----------------------------
INSERT INTO `setmeal` VALUES ('1415580119015145474', '1413386191767674881', '儿童套餐A计划', '4000.00', '1', '', '', '61d20592-b37f-4d72-a864-07ad5bb8f3bb.jpg', '2021-07-15 15:52:55', '2021-07-15 15:52:55', '1415576781934608386', '1415576781934608386', '0');

-- ----------------------------
-- Table structure for setmeal_dish
-- ----------------------------
DROP TABLE IF EXISTS `setmeal_dish`;
CREATE TABLE `setmeal_dish` (
  `id` bigint(20) NOT NULL COMMENT '主键',
  `setmeal_id` varchar(32) COLLATE utf8_bin NOT NULL COMMENT '套餐id ',
  `dish_id` varchar(32) COLLATE utf8_bin NOT NULL COMMENT '菜品id',
  `name` varchar(32) COLLATE utf8_bin DEFAULT NULL COMMENT '菜品名称 （冗余字段）',
  `price` decimal(10,2) DEFAULT NULL COMMENT '菜品原价（冗余字段）',
  `copies` int(11) NOT NULL COMMENT '份数',
  `sort` int(11) NOT NULL DEFAULT '0' COMMENT '排序',
  `create_time` datetime NOT NULL COMMENT '创建时间',
  `update_time` datetime NOT NULL COMMENT '更新时间',
  `create_user` bigint(20) NOT NULL COMMENT '创建人',
  `update_user` bigint(20) NOT NULL COMMENT '修改人',
  `is_deleted` int(11) NOT NULL DEFAULT '0' COMMENT '是否删除',
  PRIMARY KEY (`id`) USING BTREE
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COLLATE=utf8_bin COMMENT='套餐菜品关系';

-- ----------------------------
-- Records of setmeal_dish
-- ----------------------------
INSERT INTO `setmeal_dish` VALUES ('1415580119052894209', '1415580119015145474', '1397862198033297410', '老火靓汤', '49800.00', '1', '0', '2021-07-15 15:52:55', '2021-07-15 15:52:55', '1415576781934608386', '1415576781934608386', '0');
INSERT INTO `setmeal_dish` VALUES ('1415580119061282817', '1415580119015145474', '1413342036832100354', '北冰洋', '500.00', '1', '0', '2021-07-15 15:52:55', '2021-07-15 15:52:55', '1415576781934608386', '1415576781934608386', '0');
INSERT INTO `setmeal_dish` VALUES ('1415580119069671426', '1415580119015145474', '1413385247889891330', '米饭', '200.00', '1', '0', '2021-07-15 15:52:55', '2021-07-15 15:52:55', '1415576781934608386', '1415576781934608386', '0');

-- ----------------------------
-- Table structure for shopping_cart
-- ----------------------------
DROP TABLE IF EXISTS `shopping_cart`;
CREATE TABLE `shopping_cart` (
  `id` bigint(20) NOT NULL COMMENT '主键',
  `name` varchar(50) COLLATE utf8_bin DEFAULT NULL COMMENT '名称',
  `image` varchar(100) COLLATE utf8_bin DEFAULT NULL COMMENT '图片',
  `user_id` bigint(20) NOT NULL COMMENT '主键',
  `dish_id` bigint(20) DEFAULT NULL COMMENT '菜品id',
  `setmeal_id` bigint(20) DEFAULT NULL COMMENT '套餐id',
  `dish_flavor` varchar(50) COLLATE utf8_bin DEFAULT NULL COMMENT '口味',
  `number` int(11) NOT NULL DEFAULT '1' COMMENT '数量',
  `amount` decimal(10,2) NOT NULL COMMENT '金额',
  `create_time` datetime DEFAULT NULL COMMENT '创建时间',
  PRIMARY KEY (`id`) USING BTREE
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COLLATE=utf8_bin COMMENT='购物车';

-- ----------------------------
-- Records of shopping_cart
-- ----------------------------

-- ----------------------------
-- Table structure for user
-- ----------------------------
DROP TABLE IF EXISTS `user`;
CREATE TABLE `user` (
  `id` bigint(20) NOT NULL COMMENT '主键',
  `name` varchar(50) COLLATE utf8_bin DEFAULT NULL COMMENT '姓名',
  `phone` varchar(100) COLLATE utf8_bin NOT NULL COMMENT '手机号',
  `sex` varchar(2) COLLATE utf8_bin DEFAULT NULL COMMENT '性别',
  `id_number` varchar(18) COLLATE utf8_bin DEFAULT NULL COMMENT '身份证号',
  `avatar` varchar(500) COLLATE utf8_bin DEFAULT NULL COMMENT '头像',
  `status` int(11) DEFAULT '0' COMMENT '状态 0:禁用，1:正常',
  PRIMARY KEY (`id`) USING BTREE
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COLLATE=utf8_bin COMMENT='用户信息';

```



## maven项目搭建

```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>
    <parent>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-parent</artifactId>
        <version>2.4.5</version>
        <relativePath/> <!-- lookup parent from repository -->
    </parent>
    <groupId>com.reggie</groupId>
    <artifactId>reggie_take_out</artifactId>
    <version>1.0-SNAPSHOT</version>
    <properties>
        <java.version>1.8</java.version>
    </properties>
    <dependencies>

        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter</artifactId>
        </dependency>

        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-test</artifactId>
            <scope>test</scope>
        </dependency>

        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-web</artifactId>
            <scope>compile</scope>
        </dependency>

        <dependency>
            <groupId>com.baomidou</groupId>
            <artifactId>mybatis-plus-boot-starter</artifactId>
            <version>3.4.2</version>
        </dependency>

        <dependency>
            <groupId>org.projectlombok</groupId>
            <artifactId>lombok</artifactId>
            <version>1.18.20</version>
        </dependency>

        <dependency>
            <groupId>com.alibaba</groupId>
            <artifactId>fastjson</artifactId>
            <version>1.2.76</version>
        </dependency>

        <dependency>
            <groupId>commons-lang</groupId>
            <artifactId>commons-lang</artifactId>
            <version>2.6</version>
        </dependency>

        <dependency>
            <groupId>mysql</groupId>
            <artifactId>mysql-connector-java</artifactId>
            <scope>runtime</scope>
        </dependency>

        <dependency>
            <groupId>com.alibaba</groupId>
            <artifactId>druid-spring-boot-starter</artifactId>
            <version>1.1.23</version>
        </dependency>

    </dependencies>

    <build>
        <plugins>
            <plugin>
                <groupId>org.springframework.boot</groupId>
                <artifactId>spring-boot-maven-plugin</artifactId>
                <version>2.4.5</version>
            </plugin>
        </plugins>
    </build>

</project>
```

**application**

```yaml
server:
  port: 8080
spring:
  application:
    name: reggie_take_out
  datasource:
    druid:
      driver-class-name: com.mysql.cj.jdbc.Driver
      url: jdbc:mysql://localhost:3306/reggie?serverTimezone=Asia/Shanghai&useUnicode=true&characterEncoding=utf-8&zeroDateTimeBehavior=convertToNull&useSSL=false&allowPublicKeyRetrieval=true
      username: root
      password: 123456
mybatis-plus:
  configuration:
    #在映射实体或者属性时，将数据库中表名和字段名中的下划线去掉，按照驼峰命名法映射
    map-underscore-to-camel-case: true
    log-impl: org.apache.ibatis.logging.stdout.StdOutImpl
  global-config:
    db-config:
      id-type: ASSIGN_ID
```

## 前端内容导入

见资料或[github](https://github.com/Baiwuzhi/remoteIDEProjects/tree/master/reggie_take_out/src/main/resources)

****

# 后台系统登录

## 基础开发与配置

1. 创建entity包下的实体类 `employee`

   ```java
   package com.reggie.entity;
   
   import com.baomidou.mybatisplus.annotation.FieldFill;
   import com.baomidou.mybatisplus.annotation.TableField;
   import lombok.Data;
   import java.io.Serializable;
   import java.time.LocalDateTime;
   
   @Data
   public class Employee implements Serializable {
   
       private static final long serialVersionUID = 1L;
   
       private Long id;
   
       private String username;
   
       private String name;
   
       private String password;
   
       private String phone;
   
       private String sex;
   
       private String idNumber;
   
       private Integer status;
   
       private LocalDateTime createTime;
   
       private LocalDateTime updateTime;
   
       @TableField(fill = FieldFill.INSERT)
       private Long createUser;
   
       @TableField(fill = FieldFill.INSERT_UPDATE)
       private Long updateUser;
   
   }
   ```

2. 创建各种包, `config`, `controller`, `mapper`, `service`和service下的`impl`

   > config下设置`静态资源映射`

   ```java
   package com.reggie.config;
   
   @Slf4j
   @Configuration
   public class WebMvcConfig extends WebMvcConfigurationSupport {
       /**
        * 静态资源映射
        * @param registry
        */
       @Override
       protected void addResourceHandlers(ResourceHandlerRegistry registry) {
           log.info("开始进行静态资源映射");
           registry.addResourceHandler("/backend/**").
                   addResourceLocations("classpath:/backend/");
           registry.addResourceHandler("/front/**").
                   addResourceLocations("classpath:/front/");
       }
   }
   ```

3. 创建`mapper`接口, `service`接口和`实现类`, 创建`controller`

   ```java
   @Mapper
   public interface EmployeeMapper extends BaseMapper<Employee> {
   }
   ```

   ```java
   public interface EmployeeService extends IService<Employee> {
   }
   ```

   ```java
   @Service
   public class EmployeeServiceImpl extends ServiceImpl<EmployeeMapper, Employee> implements EmployeeService {
   }
   ```

   ```java
   @Slf4j
   @RestController
   @RequestMapping("/employee")
   public class EmployeeController {
   }
   ```

   后面的所有mapper,service和impl继承和实现都与此相同:

   * mapper继承的是**BaseMapper**, 泛型是**实体类**.
   * service继承的是**IService**, 泛型也是**实体类**.
   * 实现类继承的是**ServiceImpl**, 泛型有两个参数, 分别是**mapper接口, 和实体类**. 然后实现service.

4. 导入返回结果类到common包, 新建一个common包

   **此类是一个通用结果类，服务端响应的所有结果最终都会包装成此种类型返回给前端页面**

   ```java
   package com.reggie.common;
   
   import lombok.Data;
   import java.util.HashMap;
   import java.util.Map;
   
   /**
    * 通用返回结果
    * @param <T>
    */
   @Data
   public class R<T> {
   
       private Integer code; //编码：1成功，0和其它数字为失败
   
       private String msg; //错误信息
   
       private T data; //数据
   
       private Map map = new HashMap(); //动态数据
   
       public static <T> R<T> success(T object) {
           R<T> r = new R<T>();
           r.data = object;
           r.code = 1;
           return r;
       }
   
       public static <T> R<T> error(String msg) {
           R r = new R();
           r.msg = msg;
           r.code = 0;
           return r;
       }
   
       public R<T> add(String key, Object value) {
           this.map.put(key, value);
           return this;
       }
   
   }
   ```

## 编写员工登录方法

```java
@PostMapping("/login")
public R<Employee> login(HttpServletRequest request, @RequestBody Employee employee) {

    //将页面提交的密码password进行md5加密
    String password = employee.getPassword();
    password = DigestUtils.md5DigestAsHex(password.getBytes());

    //根据页面提交的用户名username查询数据库
    LambdaQueryWrapper<Employee> queryWrapper = new LambdaQueryWrapper<>();
    queryWrapper.eq(Employee::getUsername,employee.getUsername());
    Employee emp = employeeService.getOne(queryWrapper);

    //如果没有查询到则返回登陆失败结果
    if (emp == null){
        return R.error("登陆失败!");
    }

    //密码比对,如果不一致则返回登陆失败结果
    if (!emp.getPassword().equals(password)) {
        return R.error("登陆失败!");
    }

    //查看员工状态, 如果为已禁用状态,则返回员工已禁用结果
    if (emp.getStatus() == 0){
        return R.error("账号已禁用!");
    }

    //登录成功, 将员工id存入session并返回登陆成功结果
    request.getSession().setAttribute("employee",emp.getId());

    return R.success(emp);
}
```

## 后台退出功能

```java
@PostMapping("/logout")
public R<String> logout(HttpServletRequest request){
    //清理Session中保存的当前登陆员工的id
    request.getSession().removeAttribute("employee");

    return R.success("退出成功!");
}
```

## 完善登录功能

> 禁止不登陆直接访问首页,使用过滤器或者拦截器

1. 创建filter包,创建自定义过滤器

   ```java
   @WebFilter(filterName = "loginCheckFilter",urlPatterns = "/*")
   @Slf4j
   public class LoginCheckFilter implements Filter {
       //路径匹配器,支持通配符
       public static final AntPathMatcher PATH_MATCHER = new AntPathMatcher();
   
       @Override
       public void doFilter(ServletRequest servletRequest, ServletResponse servletResponse, FilterChain chain) throws IOException, ServletException {
           HttpServletRequest request = (HttpServletRequest) servletRequest;
           HttpServletResponse response = (HttpServletResponse) servletResponse;
           //获取本次请求的URI
           String requestURI = request.getRequestURI();
           log.info("拦截到请求:{}",requestURI);//断点调试查看
           //定义不需要处理的请求路径,白名单
           String[] urls = new String[]{
                   "/employee/login",
                   "/employee/logout",
                   "/backend/**",
                   "/front/**",
                   "/common/**"
           };
           //判断本次请求是否需要处理
           boolean check = check(urls, requestURI);
           //如果不需要处理，则直接放行
           if (check){
               chain.doFilter(request,response);
               return;
           }
           //判断登录状态，如果已登录，则直接放行
           if (request.getSession().getAttribute("employee") != null) {
               Long empId = (Long) request.getSession().getAttribute("employee");
               BaseContext.setCurrent(empId);
               chain.doFilter(request,response);
               return;
           }
           //如果未登录则返回未登录结果
           response.getWriter().write(JSON.toJSONString(R.error("NOTLOGIN")));
           return;
       }
   
       /**
        * 路径匹配
        * @param urls
        * @param requestURI
        * @return
        */
       public boolean check(String[] urls,String requestURI){
           for (String url : urls) {
               boolean match = PATH_MATCHER.match(url, requestURI);
               if (match){
                   return true;
               }
           }
           return false;
       }
   }
   ```

2. 在启动类上加入注解@ServletComponentScan

   ```java
   @Slf4j
   @SpringBootApplication
   @ServletComponentScan
   @EnableTransactionManagement
   public class ReggieApplication {
       public static void main(String[] args) {
           SpringApplication.run(ReggieApplication.class,args);
           log.info("项目启动成功!");
       }
   }
   ```

   ****

   

# 员工管理

## 新增员工

```java
@PostMapping
public R<String> save(HttpServletRequest request,@RequestBody Employee employee){
    log.info("新增员工,员工信息:{}",employee.toString());//断点测试

    //设置初始密码,需要加密
    employee.setPassword(DigestUtils.md5DigestAsHex("123456".getBytes()));
    employee.setCreateTime(LocalDateTime.now());
    employee.setUpdateTime(LocalDateTime.now());

    //获得当前登陆用户的id
    Long empId = (Long) request.getSession().getAttribute("employee");

    employee.setCreateUser(empId);
    employee.setUpdateUser(empId);

    employeeService.save(employee);

    return R.success("新增员工成功!");
}
```

因为username是unique(唯一,不可重复). 所以需要使用以下的**全局异常处理**

## 全局异常处理

> 在common下创建

```java
@ControllerAdvice(annotations = {RestController.class, Controller.class})
@ResponseBody
@Slf4j
public class GlobalExceptionHandler {

    /**
     * 异常处理方法
     * @return
     */
    @ExceptionHandler(SQLIntegrityConstraintViolationException.class)
    public R<String> exceptionHandler(SQLIntegrityConstraintViolationException ex){
        log.error(ex.getMessage());
        if(ex.getMessage().contains("Duplicate entry")){ //异常日志包含的关键字
            String[] split = ex.getMessage().split(" "); //正则分隔成字符串数组
            String msg = split[2]+"已存在!";
            return R.error(msg);
        }
        return R.error("未知错误!");
    }
}
```

## 分页查询

> 配置MP的`分页插件`, 在config包下.

```java
@Configuration
public class MybatisPlusConfig {
    /**
     * 分页插件
     * @return
     */
    @Bean
    public MybatisPlusInterceptor mybatisPlusInterceptor(){
        MybatisPlusInterceptor interceptor = new MybatisPlusInterceptor();
        interceptor.addInnerInterceptor(new PaginationInnerInterceptor());
        return interceptor;
    }
}
```

**分页方法**

```java
/**
 * 员工信息分页查询
 * @param page
 * @param pageSize
 * @param name
 * @return
 */
@GetMapping("/page")
public R<Page> page(int page, int pageSize, String name) {
    log.info("page = {},pageSize = {}, name = {}",page,pageSize,name);

    //构造分页构造器
    Page pageInfo = new Page(page, pageSize);

    //构造条件构造器
    LambdaQueryWrapper<Employee> queryWrapper = new LambdaQueryWrapper();
    //添加过滤条件
    queryWrapper.like(StringUtils.isNotEmpty(name),Employee::getName,name);
    //添加排序条件
    queryWrapper.orderByDesc(Employee::getUpdateTime);
    //执行查询
    employeeService.page(pageInfo,queryWrapper);
    
    return R.success(pageInfo);
}
```

**分页查询实现步骤:**

1. **返回值是泛型为`Page`的结果类, 参数为`page`, `pageSize`, 查询的`name`.**
2. **构造分页构造器**
3. **构造条件构造器**
4. **添加过滤条件**
5. **添加排序条件**
6. **执行查询并返回Page.**

## 启用/禁用员工账号

```java
@PutMapping
public R<String> update(HttpServletRequest request,@RequestBody Employee employee){
    log.info(employee.toString());
    Long empId = (Long) request.getSession().getAttribute("employee");
    employee.setUpdateTime(LocalDateTime.now());
    employee.setUpdateUser(empId);
    employeeService.updateById(employee);
    return R.success("员工信息修改成功!");
}
```

## Long型数字丢失精度问题的处理

解决方法: `扩展消息转换器`和`对象转换器(JacksonObjectMapper)`

实现原理: 

1. 提供对象转换器JacksonObjectMapper, 基于Jackson进行Java对象到json数据的转换.
2. 在WebMvcConfig配置类中扩展Springmvc的消息转换器, 在此消息转换器中使用提供的对象转换器进行java对象到json数据的转换.

> 定义在common中的JacksonObjectMapper

```java
package com.reggie.common;

/**
 * 对象映射器:基于jackson将Java对象转为json，或者将json转为Java对象
 * 将JSON解析为Java对象的过程称为 [从JSON反序列化Java对象]
 * 从Java对象生成JSON的过程称为 [序列化Java对象到JSON]
 */
public class JacksonObjectMapper extends ObjectMapper {

    public static final String DEFAULT_DATE_FORMAT = "yyyy-MM-dd";
    public static final String DEFAULT_DATE_TIME_FORMAT = "yyyy-MM-dd HH:mm:ss";
    public static final String DEFAULT_TIME_FORMAT = "HH:mm:ss";

    public JacksonObjectMapper() {
        super();
        //收到未知属性时不报异常
        this.configure(FAIL_ON_UNKNOWN_PROPERTIES, false);

        //反序列化时，属性不存在的兼容处理
        this.getDeserializationConfig().withoutFeatures(DeserializationFeature.FAIL_ON_UNKNOWN_PROPERTIES);


        SimpleModule simpleModule = new SimpleModule()
                .addDeserializer(LocalDateTime.class, new LocalDateTimeDeserializer(DateTimeFormatter.ofPattern(DEFAULT_DATE_TIME_FORMAT)))
                .addDeserializer(LocalDate.class, new LocalDateDeserializer(DateTimeFormatter.ofPattern(DEFAULT_DATE_FORMAT)))
                .addDeserializer(LocalTime.class, new LocalTimeDeserializer(DateTimeFormatter.ofPattern(DEFAULT_TIME_FORMAT)))

                .addSerializer(BigInteger.class, ToStringSerializer.instance)
                .addSerializer(Long.class, ToStringSerializer.instance)
                .addSerializer(LocalDateTime.class, new LocalDateTimeSerializer(DateTimeFormatter.ofPattern(DEFAULT_DATE_TIME_FORMAT)))
                .addSerializer(LocalDate.class, new LocalDateSerializer(DateTimeFormatter.ofPattern(DEFAULT_DATE_FORMAT)))
                .addSerializer(LocalTime.class, new LocalTimeSerializer(DateTimeFormatter.ofPattern(DEFAULT_TIME_FORMAT)));

        //注册功能模块 例如，可以添加自定义序列化器和反序列化器
        this.registerModule(simpleModule);
    }
}
```

和静态资源映射在一起的扩展消息转换器

```java
package com.reggie.config;

@Slf4j
@Configuration
public class WebMvcConfig extends WebMvcConfigurationSupport {
    /**
     * 静态资源映射
     * @param registry
     */
    @Override
    protected void addResourceHandlers(ResourceHandlerRegistry registry) {
        log.info("开始进行静态资源映射");
        registry.addResourceHandler("/backend/**").
                addResourceLocations("classpath:/backend/");
        registry.addResourceHandler("/front/**").
                addResourceLocations("classpath:/front/");
    }

    /**
     * 扩展mvc框架的消息转换器
     * @param converters
     */
    @Override
    protected void extendMessageConverters(List<HttpMessageConverter<?>> converters) {
        log.info("扩展消息转换器...");
        MappingJackson2HttpMessageConverter messageConverter = new MappingJackson2HttpMessageConverter();
        messageConverter.setObjectMapper(new JacksonObjectMapper());
        converters.add(0,messageConverter);
    }
}
```

## 员工信息修改

> 员工信息修改和启禁用员工账号共用的一个方法. 这里需要做到的是根据员工id在修改页面回显员工信息.

```java
@GetMapping("/{id}")
public R<Employee> getById(@PathVariable Long id){
    log.info("根据id查询员工信息!");
    Employee employee = employeeService.getById(id);
    if (employee != null){
        return R.success(employee);
    }
    return R.error("没有查询到对应员工信息!");
}
```

## 公共字段自动填充

> 创建时间, 更新时间, 创建用户, 更新用户, 这些都是公共字段

是mybatis plus提供的功能.

例如:

注释部分即是可省略部分

```java
@PostMapping
public R<String> save(HttpServletRequest request,@RequestBody Employee employee){
    log.info("新增员工,员工信息:{}",employee.toString());
    
    //设置初始密码,需要加密
    employee.setPassword(DigestUtils.md5DigestAsHex("123456".getBytes()));
    //employee.setCreateTime(LocalDateTime.now());
    //employee.setUpdateTime(LocalDateTime.now());

    //获得当前登陆用户的id
    //Long empId = (Long) request.getSession().getAttribute("employee");

    //employee.setCreateUser(empId);
    //employee.setUpdateUser(empId);

    employeeService.save(employee);

    return R.success("新增员工成功!");
}
```

**实现步骤:**

1. 在实体类的属性上加入@TableField注解, 指定自动填充的策略

   ```java
   @TableField(fill = FieldFill.INSERT)
   private LocalDateTime createTime;
   
   @TableField(fill = FieldFill.INSERT_UPDATE)
   private LocalDateTime updateTime;
   
   @TableField(fill = FieldFill.INSERT)
   private Long createUser;
   
   @TableField(fill = FieldFill.INSERT_UPDATE)
   private Long updateUser;
   ```

2. 按照框架要求编写元数据对象处理器, 在此类中统一为公共字段赋值, 此类需要实现MetaObjectHandler接口

   > 定义在common包下的MyMetaObjectHandler

   ```java
   //使用的ThreadLocal@Component
   @Slf4j
   public class MyMetaObjectHandler implements MetaObjectHandler {
       @Override
       public void insertFill(MetaObject metaObject) {
           log.info("公共字段自动填充[insert]...");
           log.info(metaObject.toString());
           metaObject.setValue("createTime", LocalDateTime.now());
           metaObject.setValue("updateTime",LocalDateTime.now());
           metaObject.setValue("createUser",BaseContext.getCurrent()); //使用的ThreadLocal
           metaObject.setValue("updateUser",BaseContext.getCurrent()); //使用的ThreadLocal
       }
   
       @Override
       public void updateFill(MetaObject metaObject) {
           log.info("公共字段自动填充[update]...");
           log.info(metaObject.toString());
   
           //long id = Thread.currentThread().getId();
           //log.info("线程id为:{}",id);
   
           metaObject.setValue("updateTime",LocalDateTime.now()); //使用的ThreadLocal
           metaObject.setValue("updateUser",BaseContext.getCurrent()); //使用的ThreadLocal
       }
   }
   ```

3. 基于ThreadLocal封装工具类, 用户保存和获取当前登陆用户id, 上面代码片段标注的部分

   > 一次请求对应的线程id是相同的, 就可以在线程中获取id的值到`自动填充方法`中了.

   ```java
   /**
    * 基于ThreadLocal封装工具类, 用户保存和获取当前登陆用户id
    */
   public class BaseContext {
       private static ThreadLocal<Long> threadLocal = new ThreadLocal<>();
   
       public static void setCurrent(Long id){
           threadLocal.set(id);
       }
   
       public static Long getCurrent(){
           return threadLocal.get();
       }
   }
   ```

****

# 分类管理

## 新增分类

先导入和定义实体类`Category`, `mapper`, `service`和`impl`, 还有`controller`. 与员工管理类似.

实现了`Serialzable`

```java
@Data
public class Category implements Serializable {

    private static final long serialVersionUID = 1L;

    private Long id;


    //类型 1 菜品分类 2 套餐分类
    private Integer type;


    //分类名称
    private String name;


    //顺序
    private Integer sort;


    //创建时间
    @TableField(fill = FieldFill.INSERT)
    private LocalDateTime createTime;


    //更新时间
    @TableField(fill = FieldFill.INSERT_UPDATE)
    private LocalDateTime updateTime;


    //创建人
    @TableField(fill = FieldFill.INSERT)
    private Long createUser;


    //修改人
    @TableField(fill = FieldFill.INSERT_UPDATE)
    private Long updateUser;
    
    //是否删除
    //private Integer isDeleted;

}
```

**新增分类**

```java
@RestController
@RequestMapping("/category")
@Slf4j
public class CategoryController {

    @Autowired
    private CategoryService categoryService;

    @PostMapping
    public R<String> save(@RequestBody Category category){
        log.info("category:{}",category);
        categoryService.save(category);
        return R.success("新增分类成功!");
    }
}
```

## 分类信息分类查询

```java
@GetMapping("/page")
public R<Page> page(int page, int pageSize) {
    log.info("page={},pageSize={}",page,pageSize);
    Page pageInfo = new Page(page, pageSize);
    //构造条件构造器
    LambdaQueryWrapper<Category> queryWrapper = new LambdaQueryWrapper();
    //添加过滤条件
    //queryWrapper.like(StringUtils.isNotEmpty(name),Category::getName,name);
    //添加排序条件
    queryWrapper.orderByAsc(Category::getSort);
    //执行查询
    categoryService.page(pageInfo,queryWrapper);
    return R.success(pageInfo);
}
```

## 删除分类

> 因为关联了多个表, 关联的不能删除, 所以需要自定义service

**先导入和定义需要使用的其它表的基础类和接口.**

1. **实体类Dish和Setmeal**.
2. **两个实体类所对应的mapper, service, impl**.



**自定义Service和ServiceImpl**

```java
package com.reggie.service;

public interface CategoryService extends IService<Category> {
    public void remove(Long ids);
}
```

```java
package com.reggie.service.impl;

@Service
public class CategoryServiceImpl extends ServiceImpl<CategoryMapper, Category> implements CategoryService {

    @Autowired
    private DishService dishService;

    @Autowired
    private SetMealService setMealService;

    @Override
    public void remove(Long ids) {
        LambdaQueryWrapper<Dish> dishLambdaQueryWrapper = new LambdaQueryWrapper<>();
        dishLambdaQueryWrapper.eq(Dish::getCategoryId,ids);
        int count = dishService.count(dishLambdaQueryWrapper);

        //查询当前分类是否关联了菜品
        if (count>0) {
            //已经关联菜品,抛出一个业务异常
            throw new CustomException("当前分类下关联了菜品, 不能删除!");
        }

        //查询当前分类是否关联了套餐
        LambdaQueryWrapper<Setmeal> setmealLambdaQueryWrapper = new LambdaQueryWrapper<>();
        setmealLambdaQueryWrapper.eq(Setmeal::getCategoryId,ids);
        int count1 = setMealService.count(setmealLambdaQueryWrapper);
        if (count1>0) {
            //已经关联套餐,抛出一个业务异常
            throw new CustomException("当前分类下关联了套餐, 不能删除!");
        }

        //正常删除分类
        super.removeById(ids);
    }
}
```

**定义自定义业务异常和异常类处理**

```java
package com.reggie.common;

public class CustomException extends RuntimeException{
    public CustomException(String message) {
        super(message);
    }
}
```

```java
/**
 * 自定义业务异常处理方法
 * @return
 */
@ExceptionHandler(CustomException.class)
public R<String> exceptionHandler(CustomException ex){
    log.error(ex.getMessage());
    return R.error(ex.getMessage());
}
```

**删除分类**

```java
@DeleteMapping
public R<String> delete(Long ids){
    log.info("删除分类,id为:{}",ids);
    categoryService.remove(ids);

    return R.success("删除成功!");
}
```

## 修改分类

```java
@PutMapping
public R<String> update(@RequestBody Category category){
    log.info("修改分类信息:{}",category);
    categoryService.updateById(category);
    return R.success("修改分类信息成功!");
}
```

****

# 菜品管理

## 文件上传下载

文件上传，也称为upload. 是指将本地图片、视频、音频等文件上传到服务器上，可以供其他用户浏览或下载的过程。

文件上传在项目中应用非常广泛，我们经常发微博、发微信朋友圈都用到了文件上传功能。

文件上传时，对页面的form表单有如下要求:

* method="post" 采用post方式提交数据
* enctype="multipart/form-data" 采用multipart格式上传文件
* type="file"使用input的file控件上传

举例:

```html
<form method="post" action="/common/upload" enctype="multipart/form-data">
<input name="myFile" type="file" />
<input type="submit" value="提交" />
</form>
```

服务端要接收客户端页面上传的文件，通常都会使用Apache的两个组件：

* commons-fileupload

* commons-io

Sprina框架在sprina-web包中对文件上传进行了封装，大大简化了服务端代码，我们只需要在Controller的方法中声明
一个MultipartFile类型的参数即可接收上传的文件，例如：

```java
package com.reggie.controller;

/**
 * 文件的上传和下载
 */
@RestController
@RequestMapping("/common")
@Slf4j
public class CommonController {

    @Value("${reggie.path}")
    private String basePath;

    @PostMapping("/upload")
    public R<String> upload(MultipartFile file){//参数名必须与表单中的name的值相同
        log.info(file.toString());//断点测试

        //原始文件名
        String originalFilename = file.getOriginalFilename();
        String suffix = originalFilename.substring(originalFilename.lastIndexOf("."));

        //使用UUID重新生成文件名
        String fileName = UUID.randomUUID().toString()+suffix;

        //创建一个目录对象
        File dir = new File(basePath);
        //判断当前目录是否存在
        if (!dir.exists()) {
            //目录不存在, 需要创建
            dir.mkdir();
        }
        try {
            //将临时文件转存到指定位置
            file.transferTo(new File(basePath+fileName));
        } catch (IOException e) {
            e.printStackTrace();
        }

        return R.success(fileName);
    }

    @GetMapping("/download")
    public void download(String name, HttpServletResponse response){
        try {
            //输入流,读取文件内容
            FileInputStream fileInputStream = new FileInputStream(new File(basePath+name));

            //输出流,将文件写回浏览器
            ServletOutputStream outputStream = response.getOutputStream();
            response.setContentType("image/jpeg");

            int len = 0;
            byte[] bytes = new byte[1024];
            while ((len = fileInputStream.read(bytes)) != -1){
                outputStream.write(bytes,0,len);
                outputStream.flush();
            }

            //关闭资源
            outputStream.close();
            fileInputStream.close();
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}
```

**拦截器中加入upload路径的白名单**

**application.yaml中定义保存的路径**,使用@Value接收basePath

## 新增菜品

> 涉及到两张表, dish(菜品表)和dish_flavor(菜品口味表)

导入DishFlavor实体类, 定义mapper, service和impl, 还有controller.

新增菜品需要处理的请求:

1. 菜品分类数据回显到下拉框.
2. 图片上传
3. 图片下载
4. 菜品相关数据以json形式提交到服务器.

**实现步骤:**

CategoryController定义查询list形式的分类数据

```java
@GetMapping("/list")
public R<List<Category>> list(Category category){

    //条件构造器
    LambdaQueryWrapper<Category> queryWrapper = new LambdaQueryWrapper<>();
    //添加条件
    queryWrapper.eq(category.getType() != null,Category::getType,category.getType());
    //添加排序条件
    queryWrapper.orderByAsc(Category::getSort).orderByDesc(Category::getUpdateTime);
	//执行查询
    List<Category> list = categoryService.list(queryWrapper);

    return R.success(list);

}
```

> 因为dish实体类满足不了所有的字段查询, 所以需要导入DTO, Data Transfer Object, 即数据传输对象, 一般用于展示层与服务层之间的数据传输.

**创建dto包,导入DishDto**

```java
@Data
public class DishDto extends Dish {

    private List<DishFlavor> flavors = new ArrayList<>();

    private String categoryName;

    private Integer copies;
}
```

> shService自定义新增菜品的业务方法`saveWithFlavor`, 并在serviceImpl中实现.

```java
package com.reggie.service;

public interface DishService extends IService<Dish> {
    //新增菜品, 需要操作两张表, dish,dish_flavor
    public void saveWithFlavor(DishDto dishDto);
}
```

```java
package com.reggie.service.impl;

@Service
public class DishServiceImpl extends ServiceImpl<DishMapper, Dish> implements DishService{

    @Autowired
    private DishFlavorService dishFlavorService;

    @Override
    @Transactional 
    public void saveWithFlavor(DishDto dishDto) {
        //保存菜品的基本信息
        this.save(dishDto);

        Long dishId = dishDto.getId();

        //菜品口味
        List<DishFlavor> flavors = dishDto.getFlavors();
        flavors = flavors.stream().map((item) -> {
            item.setDishId(dishId);
            return item;
        }).collect(Collectors.toList());

        //保存菜品口味数据到dish_flavor
        dishFlavorService.saveBatch(flavors);
    }
}
```

因为操作了两张表所以需要开启事务, 注意启动类中添加`@EnableTransactionManagement`

上文中的使用stream流的方式处理了DishFlavor的数据, 相当于遍历flavors设置DishId.

```java
List<DishFlavor> flavors = dishDto.getFlavors();
        flavors = flavors.stream().map((item) -> {
            item.setDishId(dishId);
            return item;
        }).collect(Collectors.toList());
```

因为DishFlavor的表数据是如下形式: 

| id                  | dish_id             | name | value                                   |
| ------------------- | ------------------- | ---- | --------------------------------------- |
| 1569978250610876419 | 1569978250585710593 | 甜味 | ["无糖","少糖","半糖","多糖","全糖"]    |
| 1569978250610876418 | 1569978250585710593 | 忌口 | ["不要葱","不要蒜","不要香菜","不要辣"] |
| 1569978250610876417 | 1569978250585710593 | 辣度 | ["不辣","微辣","中辣","重辣"]           |

**定义DishController, 注入需要的三个service.**

```java
package com.reggie.controller;

@RestController
@RequestMapping("/dish")
@Slf4j
public class DishController {
    @Autowired
    private DishService dishService;

    @Autowired
    private DishFlavorService dishFlavorService;

    @Autowired
    private CategoryService categoryService;
    
    /**
     * 新增菜品
     * @param dishDto
     * @return
     */
    @PostMapping
    public R<String> save(@RequestBody DishDto dishDto){
        log.info(dishDto.toString());
        dishService.saveWithFlavor(dishDto);

        return R.success("添加成功!");
    }
}
```

## 菜品信息分页查询

```java
/**
 * 菜品信息分页
 * @param page
 * @param pageSize
 * @param name
 * @return
 */
@GetMapping("/page")
public R<Page> page(int page,int pageSize, String name) {
    //构造分页构造器对象
    Page<Dish> dishPage = new Page<>(page,pageSize);
    Page<DishDto> dishDtoPage = new Page<>();
    //条件构造器
    LambdaQueryWrapper<Dish> queryWrapper = new LambdaQueryWrapper<>();
    queryWrapper.like(name != null,Dish::getName,name);
    queryWrapper.orderByDesc(Dish::getUpdateTime);
    //执行分页查询
    dishService.page(dishPage,queryWrapper);

    //对象拷贝
    BeanUtils.copyProperties(dishPage,dishDtoPage,"records");

    List<Dish> records = dishPage.getRecords();
    List<DishDto> list = records.stream().map((item) -> {
        DishDto dishDto = new DishDto();
        BeanUtils.copyProperties(item,dishDto);
        Long categoryId = item.getCategoryId();//分类id
        //根据id查询分类对象
        Category category = categoryService.getById(categoryId);
        if (category != null) {
        String categoryName = category.getName();
        dishDto.setCategoryName(categoryName);
        }
        return dishDto;
    }).collect(Collectors.toList());

    dishDtoPage.setRecords(list);

    return R.success(dishDtoPage);
}
```

**因为分页查询查询到的数据不完整, 需要将对象拷贝到Dto中, 再使用stream流对records进行处理.**

## 修改菜品

> 修改菜品和新增菜品类似, 也是关联的多张表, 所以需要自定义service. 
>
> 有两个自定义的service, 一个是`根据id查询菜品信息和对应的口味信息`, 用于回显, 一个是`更新菜品信息, 同时更新口味信息`.

```java
package com.reggie.service;

public interface DishService extends IService<Dish> {
    //新增菜品, 需要操作两张表, dish,dish_flavor
    public void saveWithFlavor(DishDto dishDto);

    //根据id查询菜品信息和对应的口味信息
    public DishDto getByIdWithFlavor(Long id);

    //更新菜品信息, 同时更新口味信息
    public void updateWithFlavor(DishDto dishDto);
}
```

```java
    @Override
    public DishDto getByIdWithFlavor(Long id) {
        //查询菜品基本信息
        Dish dish = this.getById(id);

        DishDto dishDto = new DishDto();
        BeanUtils.copyProperties(dish,dishDto);
        //查询当前菜品对应的口味信息
        LambdaQueryWrapper<DishFlavor> queryWrapper = new LambdaQueryWrapper<>();
        queryWrapper.eq(DishFlavor::getDishId,dish.getId());
        List<DishFlavor> flavors = dishFlavorService.list(queryWrapper);
        dishDto.setFlavors(flavors);

        return dishDto;
    }

    @Override
    public void updateWithFlavor(DishDto dishDto) {
        //更新dish表基本信息
        this.updateById(dishDto);

        //清理当前菜品对应口味数据
        LambdaQueryWrapper<DishFlavor> queryWrapper = new LambdaQueryWrapper();
        queryWrapper.eq(DishFlavor::getDishId,dishDto.getId());
        dishFlavorService.remove(queryWrapper);

        //添加当前提交过来的口味数据
        List<DishFlavor> flavors = dishDto.getFlavors();

        flavors = flavors.stream().map((item) -> {
            item.setDishId(dishDto.getId());
            return item;
        }).collect(Collectors.toList());

        dishFlavorService.saveBatch(flavors);
    }

```

> 最后是调用修改菜品

```java
@PutMapping
public R<String> update(@RequestBody DishDto dishDto){
    dishService.updateWithFlavor(dishDto);
    return R.success("修改成功!");
}
```

****

# 套餐管理

## 新增套餐

涉及两张表:

* setmeal 套餐表(节选)

  | id                  | category_id         | name          | price | status |
  | ------------------- | ------------------- | ------------- | ----- | ------ |
  | 1415580119015145474 | 1413386191767674881 | 儿童套餐A计划 | 4000  | 1      |
  | 1569238716935868417 | 1413342269393674242 | 商务套餐001   | 3000  | 1      |
  | 1569238796816388097 | 1413342269393674242 | 商务套餐002   | 4000  | 1      |

* setmeal_dish 套餐菜品关系表(节选)

  | id                  | setmeal_id          | dish_id             | name     | price    |
  | ------------------- | ------------------- | ------------------- | -------- | -------- |
  | 1415580119052894209 | 1415580119015145474 | 1397862198033297410 | 老火靓汤 | 49800.00 |
  | 1415580119061282817 | 1415580119015145474 | 1413342036832100354 | 北冰洋   | 500.00   |
  | 1415580119069671426 | 1415580119015145474 | 1413385247889891330 | 米饭     | 200.00   |

> 新增页面的套餐信息插入到setmeal表, 还需要向setmeal_dish表插入套餐和菜品关联信息.

**准备工作**

* 导入SetmealDish实体类.
* 导入SetmealDto.
* 定义SetmealDish的mapper, service, impl和controller.

**需要的请求**

* 套餐分类数据展示到下拉框中.
* 菜品分类数据展示到添加菜品窗口中.
* 菜品数据展示到添加菜品窗口中.
* 点击保存, 将套餐相关数据以json形式提交到服务器.

> DishController中定义list形式的菜品数据, 用于展示到添加菜品窗口中. 

```java
@GetMapping("/list")
public R<List<Dish>> list(Dish dish){
    //构造条件查询
    LambdaQueryWrapper<Dish> queryWrapper = new LambdaQueryWrapper<>();
    queryWrapper.eq(dish.getCategoryId() != null, Dish::getCategoryId,dish.getCategoryId());
    //添加排序条件
    queryWrapper.
            orderByAsc(Dish::getSort).
            orderByDesc(Dish::getUpdateTime);
    queryWrapper.eq(Dish::getStatus,1);
    //执行查询
    List<Dish> list = dishService.list(queryWrapper);

    return R.success(list);
}
```

> 还是自定义service, 在setmealService中.

```java
public interface SetMealService extends IService<Setmeal> {
    //新增套餐, 同时保存套餐和菜品的关联关系
    public void saveWithDish(SetmealDto setmealDto);
}
```

```java
@Service
@Slf4j
public class SetMealServiceImpl extends ServiceImpl<SetMealMapper, Setmeal> implements SetMealService {

    @Autowired
    private SetmealDishService setmealDishService;

    @Transactional
    @Override
    public void saveWithDish(SetmealDto setmealDto) {
        this.save(setmealDto);
        List<SetmealDish> setmealDishes = setmealDto.getSetmealDishes();
        setmealDishes.stream().map((item) ->{
           item.setSetmealId(setmealDto.getId());
           return item;
        }).collect(Collectors.toList());
        
        setmealDishService.saveBatch(setmealDishes);
    }
}
```

> 然后controller中调用

```java
@RestController
@RequestMapping("/setmeal")
@Slf4j
public class SetmealController {

    @Autowired
    private SetmealDishService setmealDishService;

    @Autowired
    private SetMealService setMealService;

    @Autowired
    private CategoryService categoryService;

    /**
     * 新增套餐
     * @param setmealDto
     * @return
     */
    @PostMapping
    public R<String> save(@RequestBody SetmealDto setmealDto){
        setMealService.saveWithDish(setmealDto);

        return R.success("新增套餐成功!");
    }
}
```

## 套餐信息分页查询

```java
@GetMapping("/page")
public R<Page> page(int page,int pageSize, String name){
    //分页构造器对象
    Page<Setmeal> pageInfo = new Page<>(page,pageSize);
    Page<SetmealDto> dtoPage = new Page<>();

    LambdaQueryWrapper<Setmeal> queryWrapper = new LambdaQueryWrapper<>();

    //添加查询条件
    queryWrapper.like(name != null, Setmeal::getName,name);

    //添加排序条件
    queryWrapper.orderByDesc(Setmeal::getUpdateTime);

    setMealService.page(pageInfo,queryWrapper);

    //对象拷贝
    BeanUtils.copyProperties(pageInfo,dtoPage,"records");
    List<Setmeal> records = pageInfo.getRecords();

    List<SetmealDto> dtoList = records.stream().map((item) -> {
        SetmealDto setmealDto = new SetmealDto();
        //对象拷贝
        BeanUtils.copyProperties(item,setmealDto);
        //分类id
        Long categoryId = item.getCategoryId();
        //根据分类id查询分类对象
        Category category = categoryService.getById(categoryId);
        if (category != null) {
            //分类名称
            String categoryName = category.getName();
            setmealDto.setCategoryName(categoryName);
        }
        return setmealDto;
    }).collect(Collectors.toList());

    dtoPage.setRecords(dtoList);
    return R.success(dtoPage);
}
```

## 删除套餐

> 还是现在setmeal的service中自定义删除方法

```java
public interface SetMealService extends IService<Setmeal> {
    //新增套餐, 同时保存套餐和菜品的关联关系
    public void saveWithDish(SetmealDto setmealDto);

    //删除套餐, 同时删除套餐和菜品的关联数据
    public void removeWithDish(List<Long> ids);
}
```

```java
//删除套餐, 同时删除套餐和菜品的关联数据
@Transactional
@Override
public void removeWithDish(List<Long> ids) {
    //查询套餐状态, 确定是否可以删除
    LambdaQueryWrapper<Setmeal> queryWrapper = new LambdaQueryWrapper();
    
    //添加过滤条件
    queryWrapper.in(Setmeal::getId,ids);
    queryWrapper.eq(Setmeal::getStatus,1);

    int count = this.count(queryWrapper);

    if (count > 0) {
        //不能删除抛出一个业务异常
        throw new CustomException("套餐正在售卖中, 不能删除!");
    }
    //可以删除,先删除setmeal
    this.removeByIds(ids);

    //然后删除setmealDish表中的数据
    LambdaQueryWrapper<SetmealDish> lambdaQueryWrapper = new LambdaQueryWrapper<>();
    lambdaQueryWrapper.in(SetmealDish::getDishId,ids);

    //删除关系表setmeal_dish
    setmealDishService.remove(lambdaQueryWrapper);
}
```

> 在setmealController中调用

```java
@DeleteMapping
public R<String> delete(@RequestParam List<Long> ids){
    setMealService.removeWithDish(ids);
    return R.success("套餐数据删除成功!");
}
```

