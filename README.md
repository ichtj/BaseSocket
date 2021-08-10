
## Android 项目根目录下文件 build.gradle 中添加

```groovy
allprojects {
	repositories {
		...
		maven { url 'https://www.jitpack.io' }
	}
}
```

### base_socket socket tcp/udp 通信 [![](https://jitpack.io/v/wave-chtj/BaseSocket.svg)](https://jitpack.io/#wave-chtj/BaseSocket)

```groovy
dependencies {
         //Socket TCP|UDP
         implementation 'com.github.wave-chtj:BaseSocket:1.0.1'
}
```

## base_socket socket tcp/udp 通信说明

| 编号 | 工具类        | 备注           | 实现功能     |
| ---- | ------------- | -------------- | ------------ |
| 1    | BaseTcpSocket | TCP 通讯工具类 | 发送接收回调 |
| 2    | BaseUdpSocket | UDP 通讯工具类 | 发送接收回调 |

#### base_socket 工具调用方式

```java
    //BaseUdpSocket | BaseTcpSocket tcp|udp 使用方式类似
    BaseTcpSocket baseTcpSocket = new BaseTcpSocket("192.168.1.100",8080, 5000);
    //监听回调
    baseTcpSocket.setSocketListener(new ISocketListener() {
             @Override
             public void recv(byte[] data, int offset, int size) {
                 KLog.d(TAG, "read content successful");
             }

             @Override
             public void writeSuccess(byte[] data) {
                 KLog.d(TAG, "write content successful");
             }

             @Override
             public void connSuccess() {
                 KLog.d(TAG, "The connection is successful");
             }

             @Override
             public void connFaild(Throwable t) {
                 KLog.d(TAG, "The connection is connFaild");
             }

             @Override
             public void connClose() {
                 KLog.d(TAG, "The connection is disconnect");
             }
    });
    //开启连接
    baseTcpSocket.connect(this);

    //--------------------------------------------------
    //发送数据
    baseTcpSocket.send("hello world!".getBytes());
    //关闭连接
    baseTcpSocket.close();
```