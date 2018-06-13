如何用js直接调用c/c++编写的dll
---

最近在调研如何用js直接调用c/c++编写的dll，根据浏览器的差异，使用的技术也不相同。最简单的是利用IE内置插件ActiveX（具体代码已上传到附件），js 可以通过new ActiveXObject()直接获取dll，但是我在IE浏览器上调取的时候首先提示我<br>

>Internet Explorer 已限制此网页运行 脚本或 ActiveX 控件<br>

这个问题可以通过将控件注册为安全控件避免以上窗口，我点击允许后又报了<br>

>Automation服务器不能创建对象的错误<br>

其原因有一、组件未注册，可以采用以下方法：<br>

1 将DLLTest.dll方到C:\Windows\System32下面（如果是64位系统机子，需要放到C:\Windows\SysWoW64下面）<br>
2 用管理员身份打开命令行界面,将目录切换到放置DLLTest.dll的目录（我的机子是C:\\Windows\SysWoW64） 运行 regsvr32 DLLTest.dll<br>

如果你是win10系统可以尝试[《Win10注册DLL办法》](https://blog.csdn.net/xqf222/article/details/56670786)里的方法注册dll文件<br>

然后成功调取dll文件里的方法返回“hello world”<br>

为了兼容更多浏览器，我又了解到（NPAPI、PPAPI）等非IE浏览器插件，前者很多银行已经支持NPAPI版本的安全控件，但NPAPI 却做为不安全因素被主流浏览器（Chrome、FireFox）抛弃。后者Chrome提出的名叫PPAPI的全新插件机制，运行在Chrome浏览器的沙箱环境。<br>

目前这三种方式的兼容性如下<br>
* ActiveX仅支持除了微软新出的Edge浏览器之外的所有IE浏览器<br>
* NPAPI支持360浏览器、chrome42版本以下、Opera、Firefox等浏览器，但它已经停止维护和更新了<br>
* PPAPI支持chrome42版本或以上<br>

要开发NPAPI或PPAPI插件，还需了解一些底层语言，具体如何实现，我还在研究中，欢迎给予帮助，提出不同观点！<br>


参考：<br>
[JavaScript调用dll的公用方法](https://blog.csdn.net/mengxianhua/article/details/8783146)<br>
[制作供js调用的dll并调用](https://blog.csdn.net/dylwildwolf/article/details/37695929)<br>
[PPAPI插件开发指南](https://www.cnblogs.com/fangkm/p/6628425.html)<br>




