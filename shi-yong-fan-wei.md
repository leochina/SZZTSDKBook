手动集成

1.导入aar包：

点击File --&gt; new --&gt; new module![](/assets/import.png)

选择“Import .JAR/.AAR Package”，点击next![](/assets/import_aar_package.png)



在File name里选择选择devicesapi.aar这个文件![](/assets/select_aar.png)

然后再点击finish![](/assets/import1.png)

之后就可以在Project面板看到devicesapi模块了

![](/assets/import2.png)





然后在app可运行模块下的build.gradle文件中加上 compile project\(':devicesapi'\)  再点击右上角蓝色字的Sync Now![](/assets/import3.png)

Sync Now完成后就可以使用应用型sdk的功能了。

