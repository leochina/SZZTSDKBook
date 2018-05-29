# 手动集成

1.导入aar包：

点击File --> new --> new module

![](http://7xq7oh.com1.z0.glb.clouddn.com/15271341496249.png)

选择“Import .JAR/.AAR Package”，点击next

![](http://7xq7oh.com1.z0.glb.clouddn.com/15271341631572.png)

在File name里选择选择devicesapi.aar这个文件

![](http://7xq7oh.com1.z0.glb.clouddn.com/15271341690984.png)

然后再点击finish

![](http://7xq7oh.com1.z0.glb.clouddn.com/15271341768837.png)

之后就可以在Project面板看到devicesapi模块了

![](http://7xq7oh.com1.z0.glb.clouddn.com/15271341830529.png)

然后在app可运行模块下的build.gradle文件中加上 compile project(':devicesapi') 再点击右上角蓝色字的Sync Now

![](http://7xq7oh.com1.z0.glb.clouddn.com/15271341894760.png)

Sync Now完成后就可以使用应用型sdk的功能了。

