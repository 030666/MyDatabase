@[toc]
# 一、增：数据库/表格

## 1.1  添加数据库

==sql语句:==

```sql
CREATE DATABASE 数据库名;
```

> 一般情况下，windows和macos里的mysql是不区分大小写的，因此CREATE DATABASE可以小写。但是CREATE DATABASE是关键字，所以我们用大写来和普通的字符做以区分。

==添加数据库前：==
![在这里插入图片描述](https://img-blog.csdnimg.cn/4723c73874034463a5797d15449c818a.png)
==添加数据库之后：==
![在这里插入图片描述](https://img-blog.csdnimg.cn/589c0e3e50334b3a9b30a6250f9d8977.png#pic_center)
## 1.2 进入某一个数据库
==sql语句：==

```sql
USE 数据库名;
```
这样就可以指定是在哪一个数据库中进行操作

## 1.3 添加表格
==sql语句：==

```sql
CREATE TABLE 表格名(
	列名1,
	列名2,
	列名3
);
```
>数据库创建表格时，必须定义每一列的列名和对应的数据类型
>常见的数据类型;
>1. INT:整型
>2. VARCHAR(SIZE):字符串类型(括号里面的数字用来限定字符的个数)
>3. DATE:日期类型(输入格式是年-月-日）

==添加学生信息表格：==
![在这里插入图片描述](https://img-blog.csdnimg.cn/6dbc9f93e171486fbc8e5d56a921a183.png#pic_center)
再定义了列名和数据类型的基础上还可以添加一些默认条件。
比如:

1. NOT NULL:非空（默认这一列不能为空，如果添加数据的时候如何不输入内容就会报错）
2. NULL：空（表示这一列可以为空，不输入内容默认就是NULL）
3. AUTO_INCREMENT:自动增长序列（可以实现自动递增，所以一般将主键设置为AUTO_INCREMENT）
4. COMMENT:字段注释（可以为每一列添加一个注释）
5. PRIMARY KEY:主键

==添加约束条件之后的创建表格代码：==
![在这里插入图片描述](https://img-blog.csdnimg.cn/6ddf207e5a4744188284c3365c09f21f.png#pic_center)
 ## 1.4 插入数据
 ==sql语句：==

```sql
INSERT INTO 表格名(
	列名1,列名2,列名3)
VALUES(
	数值1,数值2,数值3);
```
当我们需要同时插入多条数据到不同的数据库时还可以使用

```sql
INSERT INTO 数据库名.表格名(
	列名1,列名2,列名3)
VALUES(
	数值1,数值2,数值3);
```
>1. 即使前面加了USE进入了某一个数据库，但还是建议此时使用第二种方式，表明插入到那个数据库的哪一个表格里
>2. 一定注意数据库名和表格名中间的英文句号

==请一定要注意括号和标点符号的使用，VALUES中的字段的单引号也可以更改为双引号，但是还是建议使用单引号==
![在这里插入图片描述](https://img-blog.csdnimg.cn/db561a8493f0409ca93822414367ae15.png#pic_center)

==执行语句之后：==
![在这里插入图片描述](https://img-blog.csdnimg.cn/5a88fcf0444643ac84fc841c44bcf2a9.png#pic_center)
# 二、改：更改表格
==添加一列的语句：==

```sql
ALTER TABLE 数据库名.表格名
ADD 列名 数据类型 默认条件;
```
==修改之前的具体数据的语句：==

```sql
UPDATE 数据库名.表格名
SET 值
WHERE 条件;
```
>修改数据语句的解释：
>1. 修改数据的语句正确的顺序为UPDATE-SET-WHERE
>2. SET：用来设置更改后的具体值
>3. 要更新哪一行的数据呢？我们可以通过WHERE来定位并且加上条件来筛选

==修改之后的表格：==
![在这里插入图片描述](https://img-blog.csdnimg.cn/468f0df8608e4d5aba4213f5faa6edb7.png#pic_center)

# 三、删：数据/表格/库
## 3.1 删除某一条数据
==sql语句：==

```sql
DELETE FROM 数据库名.表格名
WHERE 条件;
```
==删除某一套数据之后：==

![在这里插入图片描述](https://img-blog.csdnimg.cn/1f44d9050f61449181098cf066b37379.png#pic_center)
## 3.2 删除某一个表格
==sql语句：==

```sql
DROP TABLE 数据库名.表格名;
```
==执行结果：==
![在这里插入图片描述](https://img-blog.csdnimg.cn/8d4f087ebc96448ba85e8fe01f6c1da5.png#pic_center)


## 3.2 删除某一个数据库
==sql语句：==

```sql
DROP DATABASE 数据库名;
```
==执行结果：==
![在这里插入图片描述](https://img-blog.csdnimg.cn/9c42723918f54c3db47b7a6901101744.png#pic_center)
# 四、查：选择/去重/排序/过滤
>这里导入下面网址里的数据，用来演示（数据分别是某个月全球的新冠感染人数和某段时间全球的新冠感染人数）
>[数据链接](https://gitee.com/dansoncut/my-sql-introductory-courseware/blob/master/Egg_database.sql#)
>
## 4.1 选择：
==查看表格的所有内容的sql语句：==

```sql
SELECT * FROM 表格名;
```
*示例：*
![在这里插入图片描述](https://img-blog.csdnimg.cn/06349f6e22464bcebe6a3ef753873512.png)

==如果要查看某几列或者某一列的内容（此时不需要*号）：==

```sql
SELECT 列名1,列名2 FROM 表格名;
```
*如果只想看国家，确诊人数，以及对应的洲名：*
![在这里插入图片描述](https://img-blog.csdnimg.cn/0f8833f5c5de40a5858a1b0501171b3f.png)
## 4.2 去重
*假如你只是想看一下数据中有多少个洲*
![在这里插入图片描述](https://img-blog.csdnimg.cn/6baa31beaf0f41a0b256d21d35faf97b.png#pic_center)
>注意此时的DISTINCT是在SELECT之后的

## 4.3 排序
==排序的sql语句：==

```sql
SELECT * FROM 表格名 ORDER BY 列名 ASC;
```
>1. 这里的ASC（Ascending）代表的是排序条件从低到高，从小到大，如果不加则会默认使用ASC。
>2. 如果将ASC换为DESC（Descending），则排序条件变为从高到低，从大到小。
>3. ASC或者DESC需要在列名的后面，ORDER BY需要在表名的后面

### 4.3.1 升序结果：
![在这里插入图片描述](https://img-blog.csdnimg.cn/3be86302195c406b8e130d4dba96679e.png#pic_center)
### 4.3.2 降序结果
![在这里插入图片描述](https://img-blog.csdnimg.cn/2700ff719381462ba9d577e64d388047.png#pic_center)
## 4.4 过滤
==过滤的sql语句：==

```sql
SELECT * FROM 表格名 WHERE 条件 ORDER BY 列名;
```
*常用的运算符：*
![在这里插入图片描述](https://img-blog.csdnimg.cn/d6cc3cf32b494f2f86755e5de62ddc0f.png#pic_center)
==如果想要查看康复数大于1000000的数据：==
![在这里插入图片描述](https://img-blog.csdnimg.cn/5cd5e3e4b51649c4a1d8df1d21b363c8.png#pic_center)
==如果想要查看康复数大于1000000并且不是巴西的数据：==

> ![在这里插入图片描述](https://img-blog.csdnimg.cn/619d25c179eb44f7910f1664e1c1e20c.png#pic_center)
> ==如果想查看区间：==
> ![在这里插入图片描述](https://img-blog.csdnimg.cn/f96a3d9997e84afe94d4f876420a9820.png#pic_center)