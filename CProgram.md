# UE4 C++ 编程说明

## GameMode

GameMode 可以认为是一个游戏的入口，或者是一张地图的入口，可以设置相应的角色等等；<br/>

代码编写的时候，官方案例都是直接在构造方法中设置 角色、控制器等等；<br/>
通常构造方法是这样的：例如有一个GameMode 为 DdzGameMode,那么在DdzGameMode.h中：
<code>
  <pre>
  UCLASS()
  class ADdzGameMode : public AGameModeBase
  </pre>
</code>
<br/>
那么在这个类中，可以包含一个构造方法：<br/>
<code>
ADdzGameMode(const FObjectInitializer& ObjectInitializer);
</code><br/>
其中的参数用于各种初始化；<br/>
构造方法的实现如下：<br/>
<code><pre>
AMatch3GameMode::AMatch3GameMode(const FObjectInitializer& ObjectInitializer) : Super(ObjectInitializer)
{
  // 此处开始设置各种成员变量，重要
	PrimaryActorTick.bCanEverTick = true;
  // 设置当前模式使用的角色，此处 APawn 代表的时候没有任何操作的角色，无法移动视窗，主要就是用于2D游戏；
	DefaultPawnClass =  APawn::StaticClass();
  // 控制器，用于传递和接收玩家的各种输入操作；
	PlayerControllerClass = AMatch3PlayerController::StaticClass();
	TileMoveSpeed = 50.0f;
	TimeRemaining = 5.0f;
	FinalPlace = 0;
}
</pre></code><br/>
