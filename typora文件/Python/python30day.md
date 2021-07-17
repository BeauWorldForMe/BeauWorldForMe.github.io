# 内容回顾

+ tcp协议的多人多次通信

  + 和一个人通信多说句话
  + 和一个人聊完再和其他人聊
  + bind 绑定一个id和端口
  + socket（）tcp协议的server
  + listen 监听，代表socket服务的开启
  + accept 和客户端建立连接的过程
  + send 直接通过连接发送消息，不需要地址
  + recv 只接收消息
  + connect 客户端、tcp协议的方法，和server端建立连接
  + close 关闭服务、连接

+ udp协议的多人通信

  + socket(type=socket.SOCK_DGRAM)
  + sendto 需要写一个对方的地址
  + recvfrom 接收消息和地址
  + close 关闭服务、连接

+ 每句话什么意思？执行到哪程序等待、阻塞、结束阻塞？

  + input() 等待
  + accept 阻塞，有客户端来和我建立连接就结束阻塞
  + recv 阻塞，直到收到对方发来的消息结束阻塞
  + recvfrom 阻塞
  + connect 阻塞，直到server端结束了对一个client的服务，开始和当前client建立连接的时候结束阻塞

+ 粘包现象

  + 什么是粘包
    + 两条或更多条分开发送的信息连在一起
  + 发生在发送端：发送间隔短，数据小，由于优化机制就合并在一起发送了
  + 发送在接收端：接收不及时，所以数据就在接收方的缓存端黏在一起了
  + 粘包发生的本质：tcp协议的传输是流式传输，数据与数据之间没有边界
  + 怎么解决粘包：自定义协议 struct模块
    + 发送端
      + 先发送四字节的数据长度     
      + 再按照长度发送数据
    + 接收端
      + 先接受四字节 知道数据长度
      + 再按照长度接收数据

+ tcp文件传输

  + ```python
    import socket
    import json
    #接收
    sk=socket.socket() #创建套接字
    sk.bind(('127.0.0.1',9000)) #绑定端口
    sk.listen()
    
    conn,_=sk.accept()
    msg=conn.recv(1024).decode('utf-8')
    print(msg)
    msg=json.loads(msg)
    
    with open(msg['filename'],'wb')as f:
        content=conn.recv(msg['filesize'])
        print('---->',len(content))
        f.write(content)
    
    
    conn.close()
    sk.close()
    ```

    ```python
    import socket
    import os
    import json
    # 发送
    sk=socket.socket() #创建套接字
    sk.connect(('127.0.0.1',9000))
    
    # 文件名、文件大小
    abs_path=r'E:\Py Project\day30\tmp'
    filename=os.path.basename(abs_path)
    filesize=os.path.getsize(abs_path)
    dic={'filename':filename,'filesize':filesize}
    str_dic=json.dumps(dic)
    sk.send(str_dic.encode('utf-8'))
    
    
    with open(abs_path,mode='rb') as f:
        content=f.read()
        sk.send(content)
    
    sk.close()
    ```

# 今日内容

+ tcp协议的自定义协议解决粘包问题

+ 验证客户端合法性

  + ![image-20200713123822700](C:\Users\15200\AppData\Roaming\Typora\typora-user-images\image-20200713123822700.png)

+ 并发的tcp协议server端---socketserver

  + ![image-20200713124302538](C:\Users\15200\AppData\Roaming\Typora\typora-user-images\image-20200713124302538.png)

    

## 代码总行数3030+41=3047行