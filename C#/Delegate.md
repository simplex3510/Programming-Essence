# 🎮 C# 콜백 아키텍처 (Delegate & Interface) 코드 분석 문제지

### [문제 1] 델리게이트 체이닝과 멀티캐스트 (코드 완성)

다음 코드는 하나의 델리게이트에 여러 메서드를 등록하여 한 번에 실행하려는 코드입니다. 주석 (A)와 (B)에 들어갈 올바른 코드를 작성하세요.

```csharp
using System;

// 1. 데미지 처리용 델리게이트 선언
public delegate void DamageHandler(int damage);

class Program
{
    static void LogDamage(int dmg) => Console.WriteLine($"[로그] {dmg}의 피해를 입었습니다.");
    static void ApplyShield(int dmg) => Console.WriteLine($"[방어구] {dmg * 0.2f}만큼의 데미지를 흡수했습니다.");

    static void Main()
    {
        // (A) DamageHandler 타입의 델리게이트 변수 handler를 선언하고 LogDamage 메서드를 할당하세요.
        __________________________________________________ ;

        // (B) handler 변수에 ApplyShield 메서드를 추가(체이닝)하세요.
        __________________________________________________ ;

        // 델리게이트 일괄 실행
        handler?.Invoke(100);
    }
}

```

---

### [문제 2] 델리게이트를 매개변수로 받는 콜백 (디버깅)

다음 코드는 무기 제작 시스템이 완료되었을 때 콜백을 호출하는 로직입니다. **컴파일 에러가 발생하는 위치 2곳**을 찾고 올바르게 수정하세요.

```csharp
using System;

public delegate void CompleteCallback(string message);

class WeaponCraftingSystem
{
    // (1) 무기 제작 메서드
    public void CraftWeapon(string weaponName, CompleteCallback onComplete)
    {
        Console.WriteLine($"{weaponName} 제작을 시작합니다...");
        Console.WriteLine($"{weaponName} 제작이 완료되었습니다!");

        // 제작 완료 후 콜백 호출
        onComplete.CraftWeapon(weaponName); // <- 에러 지점 1
    }
}

class Program
{
    static void ShowResult(string msg)
    {
        Console.WriteLine($"[알림] {msg}");
    }

    static void Main()
    {
        WeaponCraftingSystem system = new WeaponCraftingSystem();
        
        // 무기 제작 요청
        system.CraftWeapon("M4A1", ShowResult()); // <- 에러 지점 2
    }
}

```

---

### [문제 3] 인터페이스 기반 콜백 시스템 (빈칸 채우기)

C#의 델리게이트 대신 **인터페이스 계약을 활용한 콜백 방식**입니다. 빈칸 (A)와 (B)를 채워 플레이어 애니메이션이 끝났을 때 컨트롤러에 통보하는 구조를 완성하세요.

```csharp
using System;

// 콜백 전용 규격 인터페이스
public interface IAnimationEndListener
{
    void OnAnimationEnd();
}

public class PlayerAnimation
{
    // (A) 애니메이션 재생 메서드: 콜백을 받을 대상(Interface)을 매개변수로 전달받아야 합니다.
    public void Play(___________________________ listener)
    {
        Console.WriteLine("공격 애니메이션 재생 중...");
        Console.WriteLine("애니메이션 재생 완료.");

        // 애니메이션 완료 알림
        listener?.OnAnimationEnd();
    }
}

// (B) 플레이어 컨트롤러: 콜백 인터페이스를 상속(구현)해야 합니다.
public class PlayerController : ___________________________
{
    public void OnAnimationEnd()
    {
        Console.WriteLine("-> [콜백 수신] 애니메이션이 끝났으므로 다음 이동 명령을 대기합니다.");
    }
}

```

---

### [문제 4] 상태 변경 통지 델리게이트 (코드 빈칸 채우기)

플레이어의 체력이 감소할 때, `Player` 클래스가 UI 클래스를 직접 참조하지 않고 **델리게이트 통지 방식**으로 결합도를 낮춘 코드입니다. 빈칸을 완성하세요.

```csharp
using System;

public delegate void HealthChangedHandler(int currentHp, int maxHp);

public class Player
{
    public HealthChangedHandler onHealthChanged; // 체력 변경 알림 델리게이트

    private int hp = 100;
    private int maxHp = 100;

    public void TakeDamage(int damage)
    {
        hp -= damage;
        Console.WriteLine($"플레이어가 {damage}의 데미지를 입었습니다.");

        // (A) 델리게이트가 null이 아닐 때, 현재 체력(hp)과 최대 체력(maxHp)을 매개변수로 넘겨 호출하세요.
        __________________________________________________ ;
    }
}

public class HealthUI
{
    public void UpdateHPBar(int current, int max)
    {
        Console.WriteLine($"[UI 체력바] 현재 체력: {current} / {max}");
    }
}

```

---

### [문제 5] 델리게이트 안전 호출 및 예외 방지 (코드 비교)

다음 코드는 버튼이 클릭되었을 때 사운드 효과음 콜백을 실행하는 로직입니다.

```csharp
using System;

public delegate void SoundPlayHandler(string soundName);

public class Button
{
    public SoundPlayHandler onButtonClick;

    public void Click()
    {
        Console.WriteLine("버튼이 클릭되었습니다.");
        
        // 문제 발생 가능성이 있는 코드:
        onButtonClick("ClickSound.wav"); 
    }
}

```

* **문제:**
1. `onButtonClick`에 메서드가 등록되지 않았을 때(`null`일 때) 발생하는 **런타임 예외 명칭**을 쓰세요.
2. 위 `Click()` 메서드 내부를 **C#의 `?.Invoke()` 문법을 활용하여 단 한 줄의 안전한 코드**로 수정하여 작성하세요.



---

### [문제 6] 타이머 완료 콜백 (출력 결과 예측)

다음 코드가 실행되었을 때 **콘솔에 출력되는 문장들을 순서대로 작성**하세요.

```csharp
using System;

public delegate void TimerCallback();

public class CoolDownTimer
{
    public void StartTimer(TimerCallback onEnd)
    {
        Console.WriteLine("쿨다운 시작...");
        Console.WriteLine("3... 2... 1...");
        
        // 타이머 완료 후 콜백 실행
        onEnd?.Invoke();
    }
}

class Program
{
    static void Main()
    {
        CoolDownTimer timer = new CoolDownTimer();

        Console.WriteLine("스킬 버튼 누름!");
        
        timer.StartTimer(delegate {
            Console.WriteLine("★ 스킬 재사용 가능!");
        });

        Console.WriteLine("다음 행동 진행 중...");
    }
}

```

---

### [문제 7] 인터페이스 콜백 응용: 보급 상자 시스템 (코드 완성)

플레이어가 보급 상자를 열었을 때, 상자가 **인터페이스 콜백**을 통해 플레이어에게 보상을 지급하는 로직입니다. 주석 **(A)** 영역을 완성하세요.

```csharp
using System;

// 상호작용 결과 콜백 인터페이스
public interface IInteractCallback
{
    void OnInteractSuccess(string itemName);
}

public class SupplyCrate
{
    public void Open(IInteractCallback callback)
    {
        Console.WriteLine("보급 상자를 열었습니다!");
        
        // (A) 콜백 인터페이스의 메서드를 호출하여 "5.56mm 탄약통"을 전달하세요.
        __________________________________________________ ;
    }
}

public class Player : IInteractCallback
{
    // (B) IInteractCallback의 메서드를 구현하여 "탄약통 획득! 탄약 수량 +50"을 출력하도록 작성하세요.
    __________________________________________________
    __________________________________________________
    __________________________________________________
}

```

---

### [문제 8] 델리게이트와 인터페이스 콜백 종합 분석 (서술형)

다음 두 코드(A 방식, B 방식)를 읽고 질문에 답하세요.

```csharp
// [A 방식: 델리게이트 콜백]
public delegate void EventCallback();
public class SystemA {
    public void DoWork(EventCallback callback) { callback?.Invoke(); }
}

// [B 방식: 인터페이스 콜백]
public interface IEventListener {
    void OnStart();
    void OnProgress();
    void OnEnd();
}
public class SystemB {
    public void DoWork(IEventListener listener) {
        listener?.OnStart();
        listener?.OnProgress();
        listener?.OnEnd();
    }
}

```

* **질문:**
1. 단 하나의 단순한 완료 알림 기능만 필요할 때 [A 방식]이 [B 방식]보다 코드 작성 관점에서 편리한 이유를 설명하세요.
2. 작업의 시작(`OnStart`), 진행(`OnProgress`), 종료(`OnEnd`)처럼 여러 단계의 관련된 연관 이벤트들을 한 번에 전달해야 할 때 [B 방식]이 가지는 구조적 이점을 설명하세요.
