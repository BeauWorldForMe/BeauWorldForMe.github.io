# 第二章 选择语句

从单一表获取数据

运行快捷键 ctrl+shift+enter

```mysql
USE sql_store; #用这个sql_store数据库（这里需要分号）

SELECT *  #选择所有列 
FROM customers #从customers表中
WHERE customer_id = 1 #找行  
ORDER BY first_name  #排序
#需要按顺序 可以不换行 最好换
```



```mysql
SELECT 
	first_name,
    last_name,
    points,
    points * 10 + 100 AS discount_factor
FROM customers
```

![image-20210718123152510](C:\Users\15200\AppData\Roaming\Typora\typora-user-images\image-20210718123152510.png)

discount_factor类似这种变量名想要加空格 需要引号包起来

```MYSQL
SELECT DISTINCT state
FROM customers
```

DISTINCT关键字可以去重

```mysql
SELECT 
	name,
    unit_price,
    unit_price * 1.1 AS "new price"
FROM products
```

![image-20210718125953199](C:\Users\15200\AppData\Roaming\Typora\typora-user-images\image-20210718125953199.png)

## WHERE子句

```mysql
SELECT *
FROM customers
WHERE points > 3000
```

![image-20210718130128341](C:\Users\15200\AppData\Roaming\Typora\typora-user-images\image-20210718130128341.png)

```
SELECT *
FROM customers
WHERE birth_date > '1990-01-01' #日期要这种格式，还要加引号
```

## AND、OR、NOT

and优先级高，可以加括号

## IN运算符

```MYSQL
SELECT *
FROM customers
#WHERE state = 'va' OR state = 'GA' OR state = 'FL'
WHERE state IN ('VA','GA','FL') #和上面意思一样
#WHERE state NOT IN ('VA','GA','FL') 可以结合NOT使用
```

## BETWEEN和IN差不多

```MYSQL
WHERE points BETWEEN 1000 AND 3000
WHERE birth_date BETWEEN '1990-01-01' AND '2000-01-01'
```

## LIKE运算符

```MYSQL
WHERE last_name LIKE 'B%'  #百分号代表任意字符
WHERE last_name LIKE '%B%'
WHERE last_name LIKE 'B_' #下划线代表单字符
```

```MYSQL
SELECT *
FROM customers
WHERE address LIKE '%TRAIL%' OR address LIKE '%AVENUE%'
```

## REGEXP运算符 正则表达式

也可以做和LIKE一样的事

```MYSQL
SELECT *
FROM customers
WHERE last_name REGEXP 'field' 
```

'^...'表示以此字符串开头

'...$'表示以此字符串结尾

'...|...'表或者

'[gim]e'表示匹配'ge','ie','me',可以'[a-h]e'

```mysql
WHERE last_name REGEXP '[gim]e'
WHERE last_name REGEXP '[a-h]e'
```

```MYSQL
SELECT *
FROM customers
-- WHERE first_name IN ('ELKA','AMBUR') 
WHERE last_name REGEXP 'EY$|ON$' 
```

## IS NULL运算符

对于有缺失值的表

```MYSQL
WHERE phone IS NULL
WHERE phone IS NOT NULL
```

## ORDER BY子句

排序

```MYSQL
SELECT *
FROM customers
ORDER BY first_name DESC #不加DESC是默认升序
ORDER BY state,first_name  #先用一个排，再用第二个排第一个中相同的
```

mySQL可以用任意数据列排序，即使此列不在SLELCT语句中

```mysql
SELECT * ,quantity*unit_price AS total_price
FROM order_items
WHERE order_id = 2
ORDER BY total_price DESC
```

## LIMIT子句要放在最后

只要n个 `LIMIT n`

返回从第7个开始的n个 `LIMIT 6,n`

```MYSQL
SELECT *
FROM customers
ORDER BY points DESC
LIMIT 3
```

