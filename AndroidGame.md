# Android 游戏制作

## 基本信息

### 注意事项

1. 4.15 版本以下，由于 PhysX 的问题，无法编译 x86版本；

### 环境变量

1. ANDROID_HOME 指向Android SDK 目录，注意不要使用最新的SDK，因为 "android" 命令发生变化；
1. NDKROOT 环境变量 定位到NDK目录，目前推荐使用 r12b or r13b （针对UE4.15 以下）
1. ANT_HOME 指向 Apache Ant 安装目录
1. JAVA_HOME 不用多说，要指向 Java SDK 的根目录

### 打包方式

关于Android打包，需要进行如下的环境配置：<br/>

1. 下载JDK，注意如果使用Ant 1.8 那么需要设置 JAVA_HOME 环境变量；
1. 下载 Apache Ant 脚本工具，用于Android程序编译打包，推荐使用 1.9，设置环境变量 ANT_HOME;
1. 下载 Android SDK，设置 ANDROID_HOME 指向SDK目录，并且下载 Android API 19 SDK Platform!!
1. 注意 <font color="red">Android SDK 版本要低于 24，因为默认的android命令失效；确保android命令正常执行！！；</font>
1. 下载 Android Extra Support Repository
1. 下载 Google support Repository, 以及  Market_billing, market_license 支持库
1. 下载 Android NDK ，<font color="red">注意必须是 r12b 最好不要超，测试 r13可以，但是 r14b 不能用；</font>
1. 设置 NDKROOT 环境变量，指向 Android NDK 目录；

工程设置：<br/>
1. 工程项目的目标平台调整为移动设备；
1. 选择项目设置-平台-Android SDK 部分，设置目标的版本为 android-19；
1. 注意如果 版本设置到 22 或者 24，将无法编译游戏；
1. 选择项目设置-平台-Android 设置自己的包名；打包方式；
1. 设置数字签名的 keystore，别名，密码；
1. 选择打包的CPU类型，如果希望打包x86，那么需要使用源码编译虚幻4引擎；
1. 关于源码编译x86版本出现错误的问题！！
