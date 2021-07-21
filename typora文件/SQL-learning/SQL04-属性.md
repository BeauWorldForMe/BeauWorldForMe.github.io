![image-20210719101252882](C:\Users\15200\AppData\Roaming\Typora\typora-user-images\image-20210719101252882.png)

**VARCHAR(50)是变化长度的字符，数据有多长就用多少格**

**CHAR（50）是不变的，不够长就补满空格**

+ PK：主键，这列值唯一标识整个表
+ NN：非空值，整列必须所有都非空
+ AI：自动递增，会在增加数据时，把选择的列自动递增

## 插入单行

```MYSQL
INSERT INTO customers
VALUES (
	DEFAULT,
    'John',
    'Smith',
    '1990-01-01',
    '12929292929',
    'address',
    'city',
    'CA',
    DEFAULT)
```

也可以指定某些列插入,这也就可以不赋默认值和空值，也不需要按顺序，比如：

```mysql
INSERT INTO 
	customers (
        first_name,
        last_name,
        birth_date,
        address,
        city,
        state)
VALUES (
    'John',
    'Smith',
    '1990-01-01',
    'address',
    'city',
    'CA')
```

![image-20210719110810115](C:\Users\15200\AppData\Roaming\Typora\typora-user-images\image-20210719110810115.png)

## 插入多行

```mysql
INSERT INTO shippers (name)
VALUES ('SHIPPER1'),
		('SHIPPER2'),
        ('SHIPPER3')
```

![image-20210719111010533](C:\Users\15200\AppData\Roaming\Typora\typora-user-images\image-20210719111010533.png)

```mysql
INSERT INTO products (name,quantity_in_stock,unit_price)
VALUES ('ma',30,10.11),
		('ka',10,11.21),
        ('gag',4,1)
```

## 向多表插入数据

```MYSQL
SELECT LAST_INSERT_ID()
```

## 表复制

```mysql
CREATE TABLE abc AS
SELECT * FROM orders
```

选择语句也可以作为插入语句的子查询，比如：

```mysql
INSERT INTO orders_archived
SELECT *
FROM orders
WHERE order_date < '2019-01-01'
```



## 前面的练习

```mysql
USE sql_invoicing;

CREATE TABLE invoices_archived AS
SELECT 
	i.invoice_id,
    i.number,
    c.name AS client,
    i.invoice_total,
    i.payment_total,
    i.invoice_date,
    i.payment_date,
    i.due_date
FROM invoices i 
Join clients c
	USING(client_id)
WHERE payment_date IS NOT NULL
```

![image-20210721170808940](C:\Users\15200\AppData\Roaming\Typora\typora-user-images\image-20210721170808940.png)



## 更新单行

```mysql
UPDATE invoices
SET payment_total = 10,payment_date = '2019-03-01'
WHERE invoice_id = 1
```

```mysql
UPDATE invoices
SET 
	payment_total = invoice_total*0.5,
	payment_date = due_date
WHERE invoice_id = 3
```

## 更新多行

改WHERE语句

![image-20210721171814945](C:\Users\15200\AppData\Roaming\Typora\typora-user-images\image-20210721171814945.png)

上面取消勾选

```mysql
UPDATE invoices
SET 
	payment_total = invoice_total*0.5,
	payment_date = due_date
WHERE client_id = 3
```

```mysql
USE sql_store;

UPDATE customers
SET points = points + 50
WHERE birth_date < '1990-01-01'
```

## 用选择语句做UPDATE的子语句

```mysql
UPDATE invoices
SET 
	payment_total = invoice_total*0.5,
	payment_date = due_date
WHERE client_id = 
            (sELECT client_id
            FROM clients
            WHERE name = 'Myworks')
            #如果这里有多条，=要换为IN
```

## 删除行

```mysql
DELETE FROM invoices
WHERE invoice_id = 1
```

很危险，删库要跑路

## 恢复数据库

fake news！

