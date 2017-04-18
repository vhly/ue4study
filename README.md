# ue4study
UnrealEngine 4 study

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
