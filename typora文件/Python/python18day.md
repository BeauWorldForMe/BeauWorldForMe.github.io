# 今日内容

```python
'''
用代码模拟博客园系统。

项目分析：
一、首先程序启动，页面显示下面内容供用户选择：

1.请登录
2.请注册
3.进入文章页面
4.进入评论页面
5.进入日记页面
6.进入收藏页面
7.注销账号
8.退出整个程序

二、必须实现的功能：

1.注册功能要求：
    a.用户名、密码要记录在文件中
    b.用户名要求：只能含有字母或者数字，不能含有特殊字符并且确保用户名唯一。
    c.密码要求：长度要在6~16个字符之间。
    d.超过三次登录还未成功，则退出整个程序。
2.登录功能要求：
    a.用户输入用户名，密码进行登录验证。
    b.登录成功后，才可以访问3~7选项，如果没有登录或登陆不成功时访问3~7选项，不允许访问，让其先登录（装饰器）。
3.进入文章页面要求：
    a.提示欢迎xx进入文章页面。
    b.此时用户可以选择：直接写入内容，还是导入md文件。
        1.如果选择直接写内容：直接写文件名/文件内容....然后创建一个文章。
        2.如果选择导入md文件：让用户输入已经准备好的md文件的文件路径（相对路径即可，比如函数的进阶.md）,然后将md文件全部内容写入文章。
4.进入评论页面要求：
    提示欢迎xx进入评论页面。
5.进入日记页面要求：
    提示欢迎xx进入日记页面。
6.进入收藏页面要求：
    提示欢迎xx进入收藏页面。
7.注销账号要求：
    不要退出整个程序，而是将已登录的状态变成未登录的状态（访问3~7选项需要重新登录）。
8.退出整个程序要求：
    结束整个程序。
'''
status_dict={
    'username':None,
    'status':False,
}

def get_user_pwd():
    user_dict={}
    with open('register',encoding='utf-8')as f:
        for line in f:
            line_list=line.strip().split('|')
            user_dict[line_list[0].strip()]=line_list[1].strip()
    return user_dict

def login():#登录认证
    u_dict=get_user_pwd()
    count=1
    while count<4:
        username=input('请输入用户名：').strip()
        password = input('请输入密码').strip()
        if username in u_dict and password == u_dict[username]:
            print('登录成功')
            status_dict['username'] = username
            status_dict['status'] = True
            return True
        else:
            print('用户名或密码错误，重新登录')
        count += 1

def register():
    pass

def auth(f):
    '''
    你的装饰器完成，访问被装饰函数之前，写一个三次登录认证的函数
    登录成功，让其访问被装饰的函数。登录没有成功，不让访问。
    :param f:
    :return:
    '''
    def inner(*args,**kwargs):
        '''访问函数之前的操作，功能'''
        if status_dict['status']:
            ret=f(*args,**kwargs)
            '''访问函数之后的操作，功能'''
            return ret
        else:
            if login():
                ret=f(*args,**kwargs)
                return ret
    return inner()

#@auth #下面四个函数访问前，登录成功可以，没成功不能看。
def artical():
    print('欢迎访问文章页面')
#@auth
def comment():
    print('欢迎访问评论页面')
#@auth
def dairy():
    print('欢迎访问日记页面')
#@auth
def collections():
    print('欢迎访问收藏页面')
def login_out():
    pass
def quit():
    pass
# 这样可以，但是不好
# while 1:
#     print('''
#     1.请登录
#     2.请注册
#     3.进入文章页面
#     4.进入评论页面
#     5.进入日记页面
#     6.进入收藏页面
#     7.注销账号
#     8.退出整个程序
#     ''')
#     num=input('请输入序号：').strip()
#     if num=='1':
#         login()
#     elif num=='2'……

dic={
    1:login,
    2:register,
    3:artical,
    4:comment,
    5:dairy,
    6:collections,
    7:login_out,
    8:quit
}
while 1:
    print('''
        1.请登录
        2.请注册
        3.进入文章页面
        4.进入评论页面
        5.进入日记页面
        6.进入收藏页面
        7.注销账号
        8.退出整个程序
        ''')
    num=input('请输入选项：').strip()
    num=int(num)
    dic[num]()



# artical()  #inner()
# comment()  #inner()
# dairy()    #inner()
# collections() #inner()
```

+ 软件开发规范

  + 为什么要有软件开发规范？

    app、软件不可能都写在一个文件中，效率太低且不规范

  + ![image-20200628113249455](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20200628113249455.png)

  + ![image-20200628113322795](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20200628113322795.png)

  + ![image-20200628113427972](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20200628113427972.png)

  + ![image-20200628115027257](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20200628115027257.png)

  + ![image-20200628114628170](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20200628114628170.png)

  + 

## 代码总行数2085+203=2288行

