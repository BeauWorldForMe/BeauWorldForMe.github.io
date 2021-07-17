

```python
print('Hello world')
```

```python
print(1+2+3+4+5)
print((1+2+3+4+5)*3/2)
print((((1+2+3+4+5)*3/2)+100)/24)
```

```python
x=1+2+3+4+5
y=x*3/2
z=(y+100)/24
print(x,y,z)
```

+ 用户交互input

```python
username=input('请输入用户名')
password=input('请输入密码')
print(username,type(username))
print(password,type(password))
```

```python
a=input('请输入姓名：')
b=input('请输入年龄：')
c=input('请输入性别：')
print('我叫：'+a+',今年：'+b+',性别：'+c)
```

+ if语句用户登录

```python
# 嵌套的if

username=input('请输入用户名：')
password=input('请输入密码：')
code='qwer'
your_code=input('请输入验证码：')

if your_code ==code:
    if username=='汤达人'and password=='123':
        print('登录成功')
    else:
        print('账号或密码错误')
else:
    print('验证码错误')
```

