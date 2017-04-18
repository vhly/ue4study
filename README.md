# ue4study
UnrealEngine 4 study

## 入口

[编辑器基本使用](EditorUsage.md)<br/>
[蓝图使用](Blueprint.md)<br/>
[C++编程](CProgram.md)<br/>
[Android游戏](AndroidGame.md)<br/>


## Pak file encrypt and signed

Pak file is UnrealEngine game resources package file.<br/>

In newer UE4 version, encryption only for ini files in game package file.<br/>

You need set encrypt ini files = true and compress package file.<br/>

### 4.15 AES Key and Signed Key set

In UE4 4.15, AES Key can config in game project ini file.<br/>

Dont need UE4 source code and modify AES.h. It is very good for binary version.<br/>

Source code location:<br/>

Engine/Source/Programs/UnrealPak/Private/UnrealPak.cpp<br/>

Configuration:<br/>
1. In your game project folder "Config" folder, create Encryption.ini file for current games.
1. Or in your UE4 Engine \'s folder "Config", create BaseEncryption.ini file for all games.
1. INI file need include "Core.Encryption" section.
1. In Core.Encryption section add config item: SignPak=true for sign pak file.
1. In Core.Encryption section add config item: EncryptPak=true for encrypt ini file in pak file.
1. In Core.Encryption section add config item: rsa.publicexp=0xNNNNNNNN for RSA Public Exp
1. In Core.Encryption section add config item: rsa.privateexp=0xNNNNNNNN for RSA private Exp
1. In Core.Encryption section add config item: rsa.modulus=0xNNNNNNNN for RSA modulus
1. In Core.Encryption section add config item: aes.key="32characters" for AES key must more than 32 characters
<br/>
INI file example:<br/>

````
[Core.Encryption]
SignPak=true
EncryptPak=true
; RSA Signed Key's
rsa.publicexp=0x10001
rsa.privateexp=0x163c4b9641234567890c897ee0a577d6b07240909bdfd768c72d8ea8cc025bb1
rsa.modulus=0xb22e3a1512345678906e4fe505c13163c2d57968e4cbe124e5b8b843e91a8c55
; AES Key must more than 32 characters
aes.key="12345678876543211234567887654321"
````

** RSA key need 128bit key.

## About GameMode

GameMode 是一个游戏的启动或者是地图启动时的入口设置；<br/>

默认情况下，根据不同的游戏模版，创建的地图已经设置好了GameMode。<br/>

如果从空的项目创建，那么地图设置的GameMode是 None，<br/>
这样的的情况下会默认添加一个虚拟的Camera摄像机，和一个Pawn，能够进行场景导航。<br/>


GameMode 可以在地图初始化的时候，设置相应的 GameState，Pawn， Controller，以及其他。<br/>
游戏执行的时候就可以根据相应的设置，进行游戏配置。<br/>

Controller：能够控制当前地图的输入和控制，例如设置地图支持鼠标点击内容；任何用户的操作，<br/>
都可以通过 Controller 来进行控制和获取。获取事件之后，会传递给游戏世界中对应的 Actor。<br/>

Pawn：这是一种代表当前游戏主角的类型，包含眼睛可以看到游戏世界的内容，能够旋转视角。<br/>

Character：Pawn的子类，除了看到世界，还有能够移动、行走，处理游戏相关的事件。<br/>
Controller事件大部分都是由 Pawn 来实现，例如 合金弹头和魂斗罗中的游戏主角。<br/>

## About Pawn and Character

Pawn：直接的Pawn子类可以用于2D游戏或者摄像机固定的，并且不需要考虑屏幕窗口移动位置的游戏类型，<br/>
直接使用蓝图或者代码来添加一个垂直的或者水平的相机，就可以实现一种平面的游戏视图。

## About Android touch event

在项目设置中，引擎-输入 部分，有一个 Use mouse input as touch 的设置，要打开，或者直接把<br/>
当前的游戏目标平台直接调整为移动设备，这样，游戏蓝图中Actor的事件有一个 onTouchBegin 就可以作为触摸点击的入口。<br/>

## About Android Package

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

关于源码编译x86版本出现问题的解决方式：

平台：Mac OS X<br/>
NDK：r12b<br/>
V4.10 ～ V4.15<br/>

请修改 Engine/Source/ThirdParty/Physx/PxShared/include/foundation/PxPreprocessor.h<br/>
其中的代码：<br/>
<code>
  <pre>
  // static assert
  #if(defined(__GNUC__) && (__GNUC__ > 4 || (__GNUC__ == 4 && __GNUC_MINOR__ >= 7))) || (PX_PS4) || (PX_APPLE_FAMILY) || (PX_NX)
  #define PX_COMPILE_TIME_ASSERT(exp) typedef char PxCompileTimeAssert_Dummy[(exp) ? 1 : -1] __attribute__((unused))
  #else
  #define PX_COMPILE_TIME_ASSERT(exp) typedef char PxCompileTimeAssert_Dummy[(exp) ? 1 : -1]
  #endif
  </pre>
</code>
<br/>
以上的代码编译器会检测，发现数组最终会使用 -1，作为数组的长度，那么现在新的编译器会认为这是一个错误，将无法进行编译；<br/>
将 -1 修改为 0 即可，两处都需要修改；<br/>
<code>
  <pre>
  // static assert
  #if(defined(__GNUC__) && (__GNUC__ > 4 || (__GNUC__ == 4 && __GNUC_MINOR__ >= 7))) || (PX_PS4) || (PX_APPLE_FAMILY) || (PX_NX)
  #define PX_COMPILE_TIME_ASSERT(exp) typedef char PxCompileTimeAssert_Dummy[(exp) ? 1 : 0] __attribute__((unused))
  #else
  #define PX_COMPILE_TIME_ASSERT(exp) typedef char PxCompileTimeAssert_Dummy[(exp) ? 1 : 0]
  #endif
  </pre>
</code>
<br/>
