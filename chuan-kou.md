## 以下介绍串口的相关操作。



1.打开串口

要正确打开串口，先要把机器连接上串口线，然后调用serialPort的open方法打开串口，第一位参数是要打开的串口号，对于KS8223来说，通常填写“/dev/ttyUSB0”；第二位参数是波特率。

```
protected void openSerialPort(int bps) {
        //"/dev/ttyUSB0" is the default name of the serial port
        inx = serialPort.open("/dev/ttyUSB0", bps);
        if (inx >= 0) {
            tv_text.append("open serial port successfully,baud rate["+bps+"]\n");
        } else {
            tv_text.append("open serial port failure,errorCode:"+inx+"\n");
        }
    }
```



2.发送数据

发送数据调用serialPort的send方法。第一个参数是串口号，要填写上open时的返回值。第二个参数要发送的数据。第三个参数是要发送的数据的长度。

```java
protected void sendData(String sendDta) {
        byte[] data = sendDta.getBytes();
        int ret = serialPort.send(inx, data, data.length);
        if (ret >= 0) {
            tv_text.append("send data successfully\n");
        } else {
            tv_text.append("send data failure,errorCode:"+ret+"\n");
        }
    }
```



3.接收数据

接收数据调用serialPort的receive方法。第一个参数是串口号，要填写上open时的返回值。第二个参数是接收数据。第三个参数是接收数据的长度。第四个参数是接收的超时时间。

```java
protected void receiveData() {
        byte[] receiveData = new byte[256];
        int ret = serialPort.receive(inx, receiveData, receiveData.length, 60000);
        if (ret >= 0) {
            tv_text.append("received data:"
                    + StringUtil.ByteArrayToString(receiveData, ret) + "\n");
        } else {
            tv_text.append("failed to receive,errorCode:"+ret+"\n");
        }
    }
```



4.关闭串口

关闭串口调用serialPort的close方法。这里注意要确保串口正常关闭了，不然下次调用open时会异常。所以这里的处理通常都是会在onFinish\(\)是再调用多一次。

```java
protected void closeSerialPort() {
        int ret = serialPort.close(inx);
        if (ret >= 0) {
            tv_text.append(getString(R.string.public_close_success)+"\n");
        } else {
            tv_text.append(getString(R.string.public_close_fail)+" errorCode:"+ret+"\n");
        }
    }
```



