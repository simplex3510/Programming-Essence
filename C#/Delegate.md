# 🎮 C# 콜백 아키텍처: Delegate & Interface Callback 문제 8선

### 1. 델리게이트 기본 선언과 체이닝 (기본 매커니즘)

사용자 지정 델리게이트를 선언하고, 여러 개의 메서드를 하나의 델리게이트에 등록(+=)하여 연쇄적으로 호출하는 기본 콜백 체인을 작성하세요.

* **조건:**
* `int` 타입 매개변수를 하나 받고 반환형이 없는 사용자 정의 델리게이트 `delegate void DamageHandler(int damage);`를 선언하세요.
* 데미지 수치를 출력하는 메서드 2개(`LogDamage`, `ApplyShieldReduction`)를 작성하세요.
* `DamageHandler` 델리게이트 변수를 만들고, 두 메서드를 `+=` 연산자로 연결(멀티캐스트)한 뒤 델리게이트를 실행(`Invoke`)하세요.



---

### 2. 함수 매개변수로 델리게이트 전달하기 (델리게이트 콜백 기초)

메서드가 작업을 마친 후, 결과나 상태를 호출자(Caller)에게 알리기 위해 델리게이트를 매개변수로 전달받아 실행하는 콜백 패턴입니다.

* **조건:**
* 작업 완료 시 메시지를 전달받을 델리게이트 `delegate void CompleteCallback(string resultMessage);`를 선언하세요.
* `WeaponCraftingSystem` 클래스 안에 `public void CraftWeapon(string weaponName, CompleteCallback onComplete)` 메서드를 만드세요.
* 이 메서드는 제작 진행 과정을 출력한 뒤, 작업이 끝나면 전달받은 `onComplete` 콜백 메서드를 호출하면서 `"M4A1 제작 완료!"` 메시지를 넘겨주어야 합니다.



---

### 3. 인터페이스를 이용한 콜백 패턴 (Interface Callback)

C#에 델리게이트가 없던 시절이나, Java 등에서 주로 쓰이는 전통적이고 강력한 "규격 기반 콜백" 방식입니다.

* **조건:**
* 콜백 전용 인터페이스 `IAnimationEndListener`를 만들고, `void OnAnimationEnd();` 메서드를 선언하세요.
* `PlayerAnimation` 클래스를 만들고, 애니메이션 재생 메서드 `public void Play(IAnimationEndListener listener)`를 정의하세요.
* 애니메이션 출력이 끝난 후, 전달받은 `listener.OnAnimationEnd()`를 호출하세요.
* `IAnimationEndListener`를 구현하는 `PlayerController` 클래스를 만들어 애니메이션이 끝났을 때 `"다음 동작으로 이동"`이 출력되도록 연동하세요.



---

### 4. 델리게이트 방식 vs 인터페이스 방식 콜백 비교 (서술 및 비교)

두 가짓수의 콜백 방식은 실제 게임 개발 과정에서 자주 비교됩니다. 각각의 장단점을 파악했는지 검증하는 논리 문제입니다.

* **문제:**
1. **델리게이트 콜백** 방식이 인터페이스 방식에 비해 '코드 작성 및 단일 메서드 전달' 관점에서 가지는 장점을 서술하세요.
2. **인터페이스 콜백** 방식이 '여러 개의 관련 콜백 메서드(예: `OnStart`, `OnUpdate`, `OnEnd`)를 하나의 그룹으로 묶어서 전달'할 때 가지는 구조적 이점을 서술하세요.



---

### 5. 상태 변경 알림 시스템 (델리게이트 기반 이벤트 통지)

플레이어의 체력이 변경될 때, 체력 변경 사실을 플레이어 클래스가 직접 UI나 사운드 시스템에 관여하지 않고 델리게이트 통지(Notification)로 전달하도록 설계합니다.

* **조건:**
* 체력 변경 콜백 델리게이트 `delegate void HealthChangedHandler(int currentHp, int maxHp);`를 선언하세요.
* `Player` 클래스 내부에 `public HealthChangedHandler onHealthChanged;` 필드를 두세요.
* `TakeDamage(int damage)` 메서드가 실행되어 체력이 깎일 때마다, `onHealthChanged` 델리게이트가 `null`이 아니면(`!= null`) 현재 체력과 최대 체력을 매개변수로 넣어 호출하세요.
* 외부에서 UI 업데이트 메서드를 이 델리게이트에 등록하여 연동되는 모습을 `Main`에서 증명하세요.



---

### 6. 타이머 및 연사 제어 콜백 (비동기 처리 느낌의 시뮬레이션)

시간 지연이나 특정 카운트가 완료되었을 때 실행될 동작을 미리 등록해두는 시스템입니다.

* **조건:**
* `delegate void TimerCallback();`을 선언하세요.
* `CoolDownTimer` 클래스를 만들고 `public void StartTimer(int seconds, TimerCallback onCoolDownEnd)` 메서드를 만드세요.
* `for`문을 사용해 `seconds`초 동안 카운트다운을 출력(예: `"남은 시간: 3초..."`)한 뒤, 카운트가 0이 되면 `onCoolDownEnd` 콜백을 호출하세요.
* `Main`에서 이 타이머를 실행하고, 콜백으로 `"스킬 재사용 가능!"`이 출력되게 만드세요.



---

### 7. 인터페이스 콜백 기반의 무기 상호작용 시스템 (FPS 결합)

앞서 배운 인터페이스 기반 상호작용에 콜백 개념을 더해, 상호작용 결과에 따라 플레이어의 상태를 변경하는 시스템입니다.

* **조건:**
* **`IInteractCallback`** 인터페이스를 만들고, `void OnInteractSuccess(string itemName);` 메서드를 선언하세요.
* `SupplyCrate`(보급 상자) 클래스를 만들고 `public void Open(IInteractCallback callback)` 메서드를 만드세요.
* `Open` 메서드가 호출되면 상자가 열리는 연출을 출력한 뒤, `callback.OnInteractSuccess("대형 탄약통")`을 호출하세요.
* `Player` 클래스가 `IInteractCallback`을 구현하도록 만들어, 상자가 열린 후 플레이어의 탄약이 실제로 증가하는 로직을 완성하세요.



---

### 8. Null 조건 검사와 델리게이트 안전 호출 (안전성 검증)

콜백 델리게이트에 아무런 메서드도 연결되어 있지 않은 상태(`null`)에서 실행을 시도하면 `NullReferenceException` 예외가 발생하여 게임이 튕기게 됩니다.

```csharp
public delegate void SoundPlayHandler(string soundName);

public class Button
{
    public SoundPlayHandler onButtonClick;

    public void Click()
    {
        Console.WriteLine("버튼이 클릭되었습니다.");
        
        // 문제: 만약 onButtonClick에 아무 메서드도 안 들어있다면 에러가 발생합니다.
        // 안전하게 실행할 수 있는 코드 2가지 작성 방식을 작성하세요.
        onButtonClick("ClickSound.wav"); 
    }
}

```

* **문제:**
1. traditional한 `if`문 체크 방식(`!= null`)으로 위 코드를 수정하세요.
2. C#의 **`?.Invoke()`** 문법을 활용하여 단 한 줄로 안전하게 실행하는 코드로 수정하세요.
