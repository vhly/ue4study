# UE4 游戏输入

## 输入映射

## Touch输入

输入是通过 PlayerController来发送的，发送给 Pawn<br/>
Pawn 对于 Touch输入，不需要映射到某一个按键上面，直接使用BindTouch即可；<br/>
这种输入支持全屏幕输入的；<br/>
<br/>
APawn 的 SetupPlayerInputComponent 内部进行绑定<br/>

PlayerInputComponent->BindTouch(const EInputType type, UserObject*, Func);<br/>

EInputType 支持 IE_Pressed, IE_Released<br/>
Func 函数参数要求如下形式：<br/>
void Xxxxx(const ETouchIndex::Type type, const FVector vector);
