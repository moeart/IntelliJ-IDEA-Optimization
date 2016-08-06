IntelliJ IDEA 优化
======
**注意：** *文档内容目前仅针对 64 位处理器环境进行测试，32 位处理器环境请自行测试。测试之前请务必备份原 vmoptions 配置文件，以防止无法恢复正常使用状态。*

**建议：** 强烈建议于 64 位系统环境中，部署、运行 64 位开发环境。如果您运行 64 位开发环境请先部署好 64 位 JDK 环境。

针对对象
------
本文档目前主要针对于以下系列开发环境进行的优化：
- Android Studio
- IntelliJ IDEA
- WebStorm
- PHPStorm
- 其他基于 IntelliJ 的 IDE

启用 64 位环境
------
**文档中的文字置换说明：** 
- 下记描述中 ```<product>.exe``` 将代替 ```idea.exe``` ```phpstorm.exe``` ```webstorm.exe``` 等产品 32 位环境启动程序。
- 下记描述中 ```<product>.exe.vmoptions``` 与 ```<product>.exe.jdk``` 分别代替相应产品 32 位环境的 VM 或 JDK 配置文件。
- 下记描述中存在的 ```<product>64.exe``` ```<product>64.exe.vmoptions``` 以及 ```<product>64.exe.jdk``` 与上两条规则同理。

### 1. 安装 IntelliJ IDEA 所需的 JDK 环境
1. 首先从 [甲骨文（Orcale）官网下载](http://www.oracle.com/technetwork/indexes/downloads/index.html#java) 下载相应版本的 JDK，例如 ```JDK 1.8.0 x64```。
2. 打开并安装所下载的 JDK 环境安装包，请同时安装其附带的 JRE 运行环境。
3. 根据需求配置相应环境变量，例如 ```JAVA_HOME``` ```JDK_HOME``` ```JRE_HOME``` 等。（**非必备**条件）

### 2. 为 IntelliJ IDEA 启用自定义的 JDK 环境
1. 打开配置文件目录 ```用户目录\.<product>\config```，例如 ```C:\Users\MoeArtDev3\.IntelliJIdea12\config```。
2. 新建文件 ```<product>.exe.jdk```(32位) 或  ```<product>64.exe.jdk```(64位)。
3. 在文件中填写相应版本的 JDK 路径，例如 ```C:\Program Files\Java\jdk1.8.0_25```，保存后关闭。

优化启动器的 VM 参数
------
1. 打开开发环境 ```<product>.exe``` 或者 ```<product>64.exe``` 所在目录。
2. 修改 ```<product>.exe.vmoptions```(32位) 或 ```<product>64.exe.vmoptions```(64位) 配置文件。
3. 您可以参考以下两个模板（建议 8G 内存），或者参考甲骨文（Oracle）[Windows](http://docs.oracle.com/javase/8/docs/technotes/tools/windows/java.html) 、 [Linux](http://docs.oracle.com/javase/8/docs/technotes/tools/unix/java.html) 官方文档。
4. 保存配置并重新打开开发环境生效。

### 模板一 [查看来源](https://gist.github.com/P7h/4388881)
```
-server
-Xms2048m
-Xmx2048m
-XX:NewSize=512m
-XX:MaxNewSize=512m
-XX:PermSize=512m
-XX:MaxPermSize=512m
-XX:+UseParNewGC
-XX:ParallelGCThreads=4
-XX:MaxTenuringThreshold=1
-XX:SurvivorRatio=8
-XX:+UseCodeCacheFlushing
-XX:+UseConcMarkSweepGC
-XX:+AggressiveOpts
-XX:+CMSClassUnloadingEnabled
-XX:+CMSIncrementalMode
-XX:+CMSIncrementalPacing
-XX:+CMSParallelRemarkEnabled
-XX:CMSInitiatingOccupancyFraction=65
-XX:+CMSScavengeBeforeRemark
-XX:+UseCMSInitiatingOccupancyOnly
-XX:ReservedCodeCacheSize=64m
-XX:-TraceClassUnloading
-ea
-Dsun.io.useCanonCaches=false
```

### 模板二 [查看来源](https://gist.github.com/EdwardBeckett/4bbb1bcaad3f900e7305)
```
-server
-Xms2g
-Xmx2g
-Xss16m
-XX:+UseConcMarkSweepGC
-XX:+CMSParallelRemarkEnabled
-XX:ConcGCThreads=4
-XX:ReservedCodeCacheSize=128m
-XX:+AlwaysPreTouch
-XX:+TieredCompilation
-XX:+UseCompressedOops
-XX:SoftRefLRUPolicyMSPerMB=50
-Dsun.io.useCanonCaches=false
-Djava.net.preferIPv4Stack=true
-Djsse.enableSNIExtension=false
-ea
```

---

未完待续 ...

萌绘图站开发组 整理&编辑
