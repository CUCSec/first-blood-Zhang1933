# 用process monitor查看病毒进程与用火绒剑手动查杀病毒
---

 在查杀之前，禁用虚拟盘，关闭网诺连接

![禁用](/img/1.jpg)

---

## 第一步，把狗放出来

 * 单击鼠标右键选择以管理员身份运行程序
  （运行之后）
  ![dog](/img/2.PNG)

---
  ## 二.用process monitor 分析病毒
 1. 打开processtree，可发现该进程如图
  ![pro](/img/cprocess.PNG)
 
  ①于是得到一个病毒行为：创建一个12.exe与2019.exe进程。
   * 对12.exe与2019.exe进程行为监控发现创建了autorun.inf与lotto.exe文件
  ![pro](/img/cautorun.PNG)
  
 
  1. 打开porcess monitor 然后打开设置过滤器对1.exe进行进一步分析
  
  首先分析文件,设置过滤器，对1.exe文件操作进行监控
  ![doc](/img/docmuexe2.PNG)
  
  发现该进程创建了lotto.exe文件。

 3. 接下来对注册表进行分析
 
 设置过滤条件为RegCreateKey与RegSetValue如图
 ![r](/img/run.PNG)
  
   上图在注册表自启动里面添加了新的键值，即12与2019，所以每次启动计算机12.exe，2019.exe都会自启动同时开启一系列进程，进行病毒行为
 
 ![r](/img/someoprea.PNG)

 上述操作禁用注册表，禁用任务管理器，隐藏文件夹选项，同时隐藏了一些自己的文件。
 
--<font color=gray>其实是先把日志导出来，用搜索引擎查找一些path的功能，然后再在虚拟机里面对号入座</font>--

  ## 开始用火绒剑进行分析与查杀
   1. 针对所分析的开启的进程结束掉其所创建的进程及其子进程。
   ![ru](/img/k12.PNG)
   
   1. 针对文件
     将图标是文件夹但类型是应用程序的删除，先把能删的用火绒的强制删除删掉.点开autorun.inf文件
     ![auto](/img/autorun.PNG)
     从内容上可以发现里面都是关于lotto.exe启动的配置，（也就是说每点一次盘，就会启动一次病毒进程）
   2. 针对启动项
   ![pop](/img/run12.PNG)
   其创建的都删掉，如果删不掉的话就点击查看文件，将图标是文件夹但类型是应用程序的删除，先把能删的用火绒的强制删除删掉


   1. 针对上面所分析现在开始恢复注册表，任务管理器，隐藏文件夹选项
   
   *  打开组策略编辑器删除对任务管理器的禁用
  win+r组合键打开运行，在运行框中输入gpedit.msc运行
  
  * 在对话框中依次找到“用户设置\管理模板\系统\Ctrl+Alt+Del选项”；　　5、找到之后对页面右侧的“删除任务管理器”双击；　　6、双击之后就会打开“删除任务管理器”属性的设置页面，然后勾选“已禁用”
  * 然后开左侧用户配置下的“管理模版”→“系统”，然后在右侧找到并双击“阻止访问注册表编辑工具勾选“已禁用”
   

  


  


 
  
