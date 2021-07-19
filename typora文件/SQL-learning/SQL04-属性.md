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

