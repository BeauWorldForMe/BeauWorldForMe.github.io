有时是要选中多张表的

## 内连接

### JOIN关键字

+ INNER JOIN(默认，可以不加INNER)

+ OUTER JOIN

  ```mysql
  SELECT *
  FROM orders
  JOIN customers
  	ON orders.customer_id = customers.customer_id
  	#通过customer_id列连接两个表
  ```

  ```mysql
  SELECT order_id,o.customer_id,first_name,last_name
  FROM orders o #简化
  JOIN customers c
  	ON o.customer_id = c.customer_id
  ```

## 跨数据库连接

```mysql
SELECT *
FROM order_items oi
JOIN sql_inventory.products p
	ON oi.product_id = p.product_id
```

##  自连接

表和自己

比如 员工和自己的管理人员（也是员工）

```mysql
USE sql_hr;
SELECT 
	e.employee_id,
    e.first_name,
    m.first_name AS manager
FROM employees e
JOIN employees m
	ON e.reports_to = m.employee_id
```

![image-20210718173144989](C:\Users\15200\AppData\Roaming\Typora\typora-user-images\image-20210718173144989.png)

## 多表连接

```mysql
USE sql_store;
SELECT 
	o.order_id,
	o.order_date,
    c.first_name,
    c.last_name,
    os.name AS status
FROM orders o
JOIN customers c
	ON o.customer_id = c.customer_id
JOIN order_statuses os
	ON o.status = os.order_status_id
```

![image-20210718181729049](C:\Users\15200\AppData\Roaming\Typora\typora-user-images\image-20210718181729049.png)

## 复合连接条件

如果存在单一列不能识别表时

两列结合

![image-20210718181924484](C:\Users\15200\AppData\Roaming\Typora\typora-user-images\image-20210718181924484.png)

比如这样 称复合主键

```mysql
USE sql_store;
SELECT *
FROM order_items oi
JOIN order_item_notes oin
	ON oi.order_Id = oin.order_Id
    AND oi.product_id = oin.product_id
```

## 隐式连接语法 尽量别用

```mysql
SELECT *
FROM orders o
JOIN customers c
	ON o.customer_id = c.customer_id
-- --和下面一样
SELECT *
FROM orders o,customers c
WHERE o.customer_id = c.customer_id
```

## 外连接

+ LEFT JOIN 所有左表的信息会被记录 不管是不是空
+ RIGHT JOIN

## 自外连接

## USING子句

```mysql
SELECT *
FROM orders o
JOIN customers c
	-- ON o.customer_id = c.customer_id
	USING(customer_id) #有相同的名字时用
```

内连接和外连接都可

有相同的名字时用，名字不同不能用

```mysql
SELECT *
FROM order_items oi
JOIN order_item_notes oin
	USING(order_Id,product_Id)
```

## 自然连接  -危险

随缘连接

```MYSQL
SELECT *
FROM orders o
NATURAL JOIN customers c
```

## 交叉连接

```mysql
SELECT *
FROM orders o
CROSS JOIN customers c
-- 或者
SELECT *
FROM orders o,customers c 
```

返回笛卡尔积

每个人都和xx组合一遍

## 联合

```MYSQL
SELECT 
	order_id,
    order_date,
    'Active' AS status
FROM orders
WHERE order_date >= '2019-01-01'
UNION
SELECT 
	order_id,
    order_date,
    'Archived' AS status
FROM orders
WHERE order_date < '2019-01-01'
```



![image-20210718194300374](C:\Users\15200\AppData\Roaming\Typora\typora-user-images\image-20210718194300374.png)

UNION

联合多条查询，合并多个查询结果

但列数要一致

