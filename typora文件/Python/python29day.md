# 内容回顾

网络编程

+ 概念
+ B/S C/S架构
  + B/S  browser server
  + C/S   client 装客户端使用的 server远程服务器的
+ osi七层协议

# 今日内容

+ tcp协议的编程
  + 如何在连接内多和客户端说几句
  
  + 能够接收多个客户端的请求
  
  + ```python
    import socket
    
    sk=socket.socket()
    sk.bind(('127.0.0.1',9000))
    sk.listen()  #就可以等人来连接了
    
    while True:
        conn,addr=sk.accept()  #能和多个客户端握手了
        print('conn:',conn)
        while True:
            send_msg=input('>>>')
            conn.send(send_msg.encode('utf-8'))
            if send_msg.upper()=='Q':
                break
            msg=conn.recv(1024).decode('utf-8')
            if msg.upper() == 'Q':
                break
            print(msg)
        conn.close()  #挥手 断开连接
    
    sk.close()
    ```
  
    ```python
    import socket
    
    sk=socket.socket()
    sk.connect(('127.0.0.1',9000))
    
    while True:
        msg=sk.recv(1024)
        msg2=msg.decode('utf-8')
        if msg2.upper()=='Q':
            break
        print(msg,msg2)
        send_msg=input('>>>')
        sk.send(send_msg.encode('utf-8'))
        if send_msg.upper()=='Q':
            break
    
    sk.close()
    ```
  
+ udp协议的编程

  ```python
  import socket
  
  sk=socket.socket(type=socket.SOCK_DGRAM) #创建套接字
  sk.bind(('127.0.0.1',9000)) #绑定端口
  while True:
      msg,addr=sk.recvfrom(1024)  #被动等待
      print(msg.decode('utf-8'))
      msg=input('>>>')
      sk.sendto(msg.encode('utf-8'),addr)
  ```

  ```python
  import socket
  
  sk=socket.socket(type=socket.SOCK_DGRAM) #创建套接字
  server=(('127.0.0.1',9000))
  
  while True:
      msg = input('>>>')
      if msg.upper()=='Q':
          break
      sk.sendto(msg.encode('utf-8'),server)
      msg=sk.recv(1024).decode('utf-8')
      if msg.upper()=='Q':
          break
      print(msg)
  ```

+ 粘包现象

  + 两条连续发送的数据黏在一起了
  + ![image-20200712130413576](C:\Users\15200\AppData\Roaming\Typora\typora-user-images\image-20200712130413576.png)
  + 只出现在tcp协议中
    + 因为tcp协议 多条消息之间没有边界，并且还有一大堆优化算法
    + 发送端：两条消息都很短，发送的间隔时间也非常短
    + 接收端：多条消息由于没有及时接收，而在接收方的缓存短 堆在一起导致的粘包现象
  + 网络最大带宽限制 MTU=1500字节
  + tcp发多大都行 因为会在中途拆分

+ struct模块

  + ![image-20200712132651341](C:\Users\15200\AppData\Roaming\Typora\typora-user-images\image-20200712132651341.png)

+ 选课系统讲解I



## 代码总行数2856+174=3030行