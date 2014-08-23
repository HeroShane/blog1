---
layout: post
title: mongodb知识整合
categories:
    - 数据库
    - mongodb
tags:
    - mongodb
excerpt: mongodb知识整合    
---

## 数据库
```sh
1、显示所有数据的列表（使用mongodb，不需要创建数据库）
show dbs

2、显示当前数据库对象或者集合
db

3、连接到一个特定的数据库
use zky
```
>**注：**数据库名字不能包含"$"，"system"作为系统保留字符串不能作为数据库名字

## 文档
文档类比关系型数据库中每一行数据。多个键及其关联的值有序的放置在一起就是文档。在mongodb中使用一种类型json的bson存储数据。bson可以理解为在json基础上添加了一些json中没有的数据类型。
* 概念整合
<table width="100%">
	<tbody>
		<tr>
			<th width="50%">关系数据库</th>
			<th width="50%">mongodb</th>
		</tr>
		<tr>
			<td>
				<code class="v-code">Table</code>
			</td>
			<td>
				<code class="v-code">Collection</code>
			</td>
		</tr>
		<tr>
			<td>
				<code class="v-code">Column</code>
			</td>
			<td>
				<code class="v-code">Key</code>
			</td>
		</tr>
		<tr>
			<td>
				<code class="v-code">Value</code>
			</td>
			<td>
				<code class="v-code">Value</code>
			</td>
		</tr>
		<tr>
			<td>
				<code class="v-code">Records/Rows</code>
			</td>
			<td>
				<code class="v-code">Document/Object</code>
			</td>
		</tr>
	</tbody>
</table>

* 数据类型
<table width="100%">
	<tbody>
		<tr>
			<th width="20%">数据类型</th>
			<th width="80%">描述</th>
		</tr>
		<tr>
			<td>
				<code class="v-code">string</code>
			</td>
			<td></td>
		</tr>
		<tr>
			<td>
				<code class="v-code">integer</code>
			</td>
			<td></td>
		</tr>
		<tr>
			<td>
				<code class="v-code">boolean</code>
			</td>
			<td></td>
		</tr>
		<tr>
			<td>
				<code class="v-code">double</code>
			</td>
			<td></td>
		</tr>
		<tr>
			<td>
				<code class="v-code">null</code>
			</td>
			<td>不是0，也不是空</td>
		</tr>
		<tr>
			<td>
				<code class="v-code">array</code>
			</td>
			<td>数组</td>
		</tr>
		<tr>
			<td>
				<code class="v-code">object</code>
			</td>
			<td>对象型，程序中被使用的实体。可以是一个值，变量，函数或者是数据结构</td>
		</tr>
		<tr>
			<td>
				<code class="v-code">timestamp</code>
			</td>
			<td>前32位是utc时间，后32位是这一秒内的计数值</td>
		</tr>
		<tr>
			<td>
				<code class="v-code">ObjectIDs</code>
			</td>
			<td>在mongodb中需要使用唯一的关键字_id来标识它们。几乎每一个mongodb文档都使用_id作为第一属性。_id可以是任何类型，最常做法是使用ObjectId类型</td>
		</tr>
	</tbody>
</table>

## 集合
集合就是一组文档的组合，如果将文档类比成数据库中的行，那么集合就可以类比成数据库的表。
```sh
下面的文档可以同时存入到同一个文档中：
{"name":"xxk"}
{"name":"ssh" , "age":"34"}
```
>**注：**当第一个文档插入时，集合就会被创建。

## capped collections
需要显式创建一个capped collection，指定一个collection的大小，单位是字节。collection的数据存储空间是提前分配的。
```sh
> db.createCollection("mycoll" , {capped:true , size:1000000})
```
## 元数据
<table width="100%">
	<tbody>
		<tr>
			<th width="30%">集合命名空间</th>
			<th width="70%">描述</th>
		</tr>
		<tr>
			<td>
				dbname.system.namespace
			</td>
			<td>
				列出所有名字空间
			</td>
		</tr>
		<tr>
			<td>
				dbname.system.profile
			</td>
			<td>
				数据库概要信息
			</td>
		</tr>
		<tr>
			<td>
				dbname.system.indexes
			</td>
			<td>
				列出所有索引
			</td>
		</tr>
		<tr>
			<td>
				dbname.system.users
			</td>
			<td>
				列出可访问数据库的用户
			</td>
		</tr>
		<tr>
			<td>
				dbname.local.sources
			</td>
			<td>
				复制对端(slave)的服务器信息和状态
			</td>
		</tr>
	</tbody>
</table>
* 在{{system.indexes}}插入数据，可以创建索引；
* {{system.users}}是可修改的；
* {{system.profile}}是可删除的。

## 启动mongodb服务
默认情况下，mongodb的启动端口为27017,28017为mongodb的web用户界面。

## 增(insert)删(delete)改(remove)
* 插入
```sh
1、数据库切换
> use mudb switch to db mydb
2、定义一个文档
> document=({... ...})
3、往集合中插入数据
> db.userdetails.insert(document);
4、查看集合中的数据
> db.userdetails.find();
```
* 更新
```sh
> db.collection.update(criteria , objNew , upsert , multi)
```
1. criteria：查询条件
2. objNew：更新内容
3. upsert：倘若查询不到匹配信息，是否插入，默认为false
4. multi：默认为false，若为true就按照查询条件查出多条记录，全部更新
```sh
1、只更新第一条记录：
> db.test0.update({"count" : ($gt : 1)} , { $set : {"test2" : "ok"}});
2、全部更新:
> db.test0.update({ "count" : { $gt : 3}} , { $set : { "test2" : "ok" }} , false , true)
3、只添加第一条：
> db.test0.update({"count" : {$gt : 4}} , { $set : {"test5" : "ok"}} ,true , false)
4、全部添加
> db.test0.update({"count" : { $gt : 5}} , { $inc : {"count" : "1"}} , true , true)
5、只更新第一条记录
> db.test0.update({"count" : { $gt : 5}} , { $inc : {"count" : "1"}} , false , false)
```
* 删除
```sh
1、删除特定数据：
> db.test0.remove({"userid" : "00001"})
2、删除集合:
> db.test0.drop()
3、删除数据库:
> db.dropDatabase()
```
>**注：**在删除数据库之前查看当前数据库再进行数据库删除操作

## 查询
* 从集合中获取数据
```sh
> db.test0.find();
> select * from test0;
```
* 通过特定条件读取数据
```sh
> db.test0.find({"eduction" : "m.c.a"})
> select * from test0 where education="m.c.a";
```
* $gt、$gte、$lt、$lte
```sh
> db.test0.find({age : {$gt :22}})
> select * from test0 where age > 22;

> db.test0.find({age : {$gte :22}})
> select * from test0 where age >= 22;

> db.test0.find({age : {$lt :22}})
> select * from test0 where age < 22;

> db.test0.find({age : {$lte :22}})
> select * from test0 where age <= 22;

> db.test0.find({age : {$lt : 24 , $gt : 17}})
```

## 排序、索引、聚合
* 排序：1为升序排序，-1为降序排序
```sh
1、基本使用
> db.test0.find().sort({key : 1})
2、test0集合中数据按照title降序排序：
> db.test.find({},{"title":1 , _id:0}.sort({"title":-1}))
```
* 索引：1为指定按升序创建索引，-1指定按降序来创建索引
```sh
1、基本使用
> db.test0.ensureIndex({"title":1})
2、使用多个字段创建索引
> db.test0.ensureIndex({"title":1 , "desc":-1})
3、在后台创建索引
> db.test0.ensureIndex({open:1 , close:-1} , {background:true})
```
* 聚合
```sh
1、$group
> db.test0.aggregate([{$group : {_id : "$by_user" , num_tutorial : {$sum : 1}}}]);
> select by_user , count(*) from test0 group by  by_user;

2、$sun
> db.test0.aggregate([{$group：{_id:"$by_user" , num_tutorial:{$sum:"$likes"}}}])

3、$avg
> db.test0.aggregate([{$group:{_id:"$by_user" , num_tutorial:{$avg:"$likes"}}}])

4、$min
> db.test0.aggregate([{$group:{_id:"$by_user" , num_tutorial:{$min:"$likes"}}}])

5、$max
> db.test0.aggregate([{$group:{_id:"$by_user" , num_tutorial:{$max:"$likes"}}}])

6、$push：在结果文档中插入值到一个数组中
> db.test0.aggregate([{group:{_id:"$by_user" , url:{$push:"$url"}}}])

7、$addToSet：在结果文档中插入值到一个数组中，但不创建副本
> db.test0.aggregate([{group:{_id:"$by_user" , url:{$addToSet:"$url"}}}])

8、$first
> db.test0.aggregate([{group:{_id:"$by_user" , first_url:{$first:"$url"}}}])

9、$last
> db.test0.aggregate([{group:{_id:"$by_user" , last_url:{$last:"$url"}}}])
```
* 管道的概念
mongodb聚合管道将文档处理完毕之后再传递给下一个管道处理。表达式是无状态的，只能用于计算当前集合管道的文档，不能处理其他文档。
1. $project：修改输入文档的结构。可以用来重命名、增加或者删除域，也可以用于创建计算结果及嵌套文档。
2. $match：用于过滤数据，只输出符合条件的文档。
3. $limit：限制管道返回的文档数目。
4. $skip：在聚合管道中跳过指定数量的文档，返回剩余的文档。
5. $unwind：将文档中某一个数组类型字段拆分成多条，每条包含数组中的一个值。
6. $group：将集合中文档分组，用于统计结果
7. $sort：输出后排序
8. $geoNear

## 关系

以用户与地址（一对多）进行说明：

* 嵌入关系：把用户地址嵌入到用户的文档中
```sh
> db.users.findOne({"name":"zky"} , {"address":1})
```
>**注：**这种数据结构的缺点是，如果用户和用户地址不断增加，数据量不断变大，会影响读写性能。

* 引用关系：吧用户数据文档和用户地址数据文档分开，通过文档的id来建立关系
```sh
> var result = db.users.findOne({"name":"zky"} , {"address_ids":1})
> var address = db.users.find({"_id" : {"$in" : result["address_ids"]}})
```

## 数据库引用
1. $ref：集合名称
2. $id：引用的id
3. $db：数据库的名称
```sh
> var user = db.users.findOne({"name":"zky"})
> var dbRef = user.address
> db[dbRef.$ref].findOne({"_id":(dbRef.$id)})
```
>以上实例反悔了address_home集合中的地址数据

## 查询分析

* explain()：提供了查询信息，使用索引即查询统计。有利于我们对索引的优化：

参数分析:
1. indexOnly：字段为true，表示我们使用了索引
2. cursor：通过这个名称可以查看当前数据库下的system.indexes集合
3. n：当前查询返回的文档数量
4. nscanned/nscannedObjects:表名当前查询一共扫描了多少个文档，这个数量和返回文档数量越接近越好
5. millis：当前查询所需时间
6. indexBounds：当前查询具体时间

## 原子操作
所谓原子操作就是，这个文档要么保存到mongodb，要么不保存.

原子操作常用命令：
1. $set：用来指定一个键，若键不存在就创建。{$set : {field : value}}
2. $unset：用来删除一个键。{$unset : {field : 1}}
3. $inc：可以对文档的某个值为数字型的键进行增减操作。{$inc : {field : value}}
4. $push：  把value追加到field之中，field必须是数组。如果field不存在，会新增一个数组类型。{$push:{field : value}}
5. $pull：从数组中删除一个等于value的值。{$pull : {field : _value}}
6. $addToSet：增加一个值到数组中，而且只有这个值不存在于数组之中才会增加。
7. $pop：删除数组中第一个或最后一个元素。{$pop : {field : 1}}
8. $rename：修改字段名称。{$rename : {old_field_name : new_field_name}}

## 正则表达式

* 查找特定字段
```sh
> db.posts.find({post_text:{$regex:"..."}})
> db.posts.find({post_text:/.../})
```

* 不区分大小写的正则表达式
```sh
> db.posts.find({post_text:{$regex:"..." , $options:"$i"}})
```
* 数组元素使用正则表达式
```sh
> db.posts.find({tags:{$regex:"..."}})
```
