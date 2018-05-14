初始化

可以参照PosDemo的位于com.szzt.posdemo.model包下面的SDKManager类，该类示范了如何初始化DeviceTransManager并且获取如打印机、密码键盘、磁条读卡器、接触读卡器和非接触读卡器等资源。

然后在自身工程的Application类里面初始化SDKManager

```java
public class SzztApplication extends Application{

    @Override
    public void onCreate() {
        super.onCreate();
        init();
    }

    private void init() {
        //DeviceTransManager and SZZTSystemManager must be initialized when app starts
        SDKManager.getInstance(this);
    }
}
```

打印机相关功能可以在PrinterExampleActivity这里看到：

1.打开打印机

```java
//返回ret >= 0 时表示打开打印机设备成功
    protected void openDevice() {
        int ret = szztPrinter.open();
        if (ret >= 0) {
            tv_text.append("open printer successfully\n");
        } else {
            tv_text.append("failed to open printer,errorCode:"+ret+"\n");
        }
    }
```

2.获取打印机状态

```java
//获取打印机的状态
    protected boolean getPrinterStatue() {
        int ret = szztPrinter.getStatus();
        if(ret == SZZTPrinter.STATUS_OK)
        {
            tv_text.append("printer normal\n");
            return true;
        }else if(ret == SZZTPrinter.STATUS_NO_PAPER){
            tv_text.append("prnter out of paper\n");
        }else if(ret == SZZTPrinter. STATUS_HARDERR)
        {
            tv_text.append("hardware error\n");
        }else if(ret == SZZTPrinter.STATUS_OVERHEAT)
        {
            tv_text.append("printer overheating\n");
        }else if(ret == SZZTPrinter.STATUS_LOWVOL)
        {
            tv_text.append("Low voltage\n");
        }else if(ret == SZZTPrinter.STATUS_PAPERJAM)
        {
            tv_text.append("jam\n");
        }else if(ret == SZZTPrinter.STATUS_BUSY)
        {
            tv_text.append("printer busy\n");
        }else if (ret == 242) {
            tv_text.append("printer is closed\n");
        }else if (ret == DEVICE_NOT_OPEN) {
            tv_text.append("printer is not opened\n");
        }
        else{
            tv_text.append("unknown exception["+ret+"]\n");
        }
        return false;
    }
```

3.打印图片

打印图片可以调用addImg\(bitmap\)这个方法，这里注意，参数必须是bitmap，bitmap在5M之内。再调用startPrint就可以开始打印了。以下是示例：

```java
/**
     * the source image must be a monochrome bitmap
     */
    protected void printerImg() {
        if (false == getPrinterStatue()) return;
        new Thread(new Runnable() {

            @Override
            public void run() {
                try {
                    InputStream is = PrinterExampleActivity.this.getAssets().open("jhlogo.png");
                    Bitmap bitmap = BitmapFactory.decodeStream(is);
                    szztPrinter.addImg(bitmap);
                    szztPrinter.addFeedPaper(2,0);
                    szztPrinter.startPrint(printListenrer);
                } catch (Exception e) {
                    e.printStackTrace();
                }
            }
        }).start();
    }
```

4.打印二维码、文字等都可以参考这类的代码。





## 银行卡读取，Pboc相关：

银行卡的读取示例可以进入到消费的流程去看。

