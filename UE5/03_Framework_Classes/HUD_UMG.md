# UMG(Unreal Motion Graphics)

<br/>

### HUD   

Canvas 기반 HUD(예전방식)   
UMG(Unreal Motion Graphics)   
-> 요즘 씀 (Widget Blueprint 사용)   
프로젝트이름.Build.cs 파일에 들어가서 UMG 등록을 해줘야 한다.(C# 코드)   

<br/>

```c#
PublicDependencyModuleNames.AddRange(new string[] { 
	"Core", 
	"CoreUObject", 
	"Engine", 
	"InputCore", 
	"EnhancedInput",
	"UMG" // 여기 이부분 추가
  });
```

<br/>

***

<br/>

### Button   

<br/>

```cpp
// 헤더파일에 #include "Components/Button.h"

// Widget의 버튼을 찾아서 각각 캐스팅해준다.
UButton* StartButton = Cast<UButton>(MainMenuWidgetInstance->GetWidgetFromName(TEXT("StartButton")));
UButton* RestartButton = Cast<UButton>(MainMenuWidgetInstance->GetWidgetFromName(TEXT("RestartButton")));
		
if (StartButton && RestartButton)
{
	if (bIsRestart)
	{
    // Restart일때 StartButton은 사라지게 하고 RestartButton만 보이게 한다.
		StartButton->SetVisibility(ESlateVisibility::Collapsed);
		RestartButton->SetVisibility(ESlateVisibility::Visible);

		if (UTextBlock* ButtonText = Cast<UTextBlock>(MainMenuWidgetInstance->GetWidgetFromName(TEXT("RestartButtonText"))))
		{
			ButtonText->SetText(FText::FromString(TEXT("Restart")));

		}
	}
	else
	{
    // 위와 반대로
		StartButton->SetVisibility(ESlateVisibility::Visible);
		RestartButton->SetVisibility(ESlateVisibility::Collapsed);

		if (UTextBlock* ButtonText = Cast<UTextBlock>(MainMenuWidgetInstance->GetWidgetFromName(TEXT("StartButtonText"))))
		{
			ButtonText->SetText(FText::FromString(TEXT("Start")));
		}
	}
}
```

<br/>

***

<br/>

### Animation 실행 코드

<br/>

```cpp
// 에디터에서 만든 PlayGameOverAnim을 실행
UFunction* PlayAnimFunc = MainMenuWidgetInstance->FindFunction(FName("PlayGameOverAnim"));
if (PlayAnimFunc)
{
	MainMenuWidgetInstance->ProcessEvent(PlayAnimFunc, nullptr);
}
```

