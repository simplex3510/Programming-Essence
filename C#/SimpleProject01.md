# 🎯 FPS 프로젝트 과제: "텍스트 기반 택티컬 웨폰 시스템"

FPS 게임의 핵심인 총기(추상 클래스), 부착물/모드(중첩 클래스), 상호작용 가능한 물체(인터페이스)를 직접 코드로 설계하고 구동하는 시스템 개발 과제입니다.

---

## 🛠️ 과제 요구 사항 (기능 명세)

### 1. 추상 클래스 활용: `Firearm` (총기 기본 뼈대)

모든 총기의 공통 속성과 기능을 담은 부모 추상 클래스입니다.

* **프로퍼티/필드:** `string Name`(총기 이름), `int MaxAmmo`(최대 장탄수), `int CurrentAmmo`(현재 남은 총알)
* **일반 메서드:** `public void Reload()` -> "장전 중..." 출력 후 `CurrentAmmo`를 `MaxAmmo`로 채우는 공통 로직.
* **추상 메서드:** `public abstract void Fire();` -> 총기 종류(라이플, 샷건 등)마다 격발 방식과 소리가 다르므로 자식에서 강제 구현.

### 2. 중첩 클래스 활용: 부착물 또는 사격 모드 정보 (`FireMode`)

총기 내부에서만 밀접하게 사용되는 사격 모드(단발, 연사) 데이터를 외부로부터 은닉합니다.

* `Firearm` 클래스 내부에 `private` 또는 `protected`로 중첩 클래스 `FireMode`를 선언하세요.
* `FireMode`는 `string modeName`("단발", "연사")과 `int burstCount`(한 번 클릭에 나가는 총알 수)를 가집니다.
* 자식 총기들은 생성될 때 이 중첩 클래스를 내부에서 생성하여 자신의 사격 모드를 설정합니다.

### 3. 인터페이스 활용: `IInteractable` (상호작용 시스템)

FPS 게임에서 플레이어가 F키를 눌러 문을 열거나, 상자를 열거나, 바닥의 무기를 줍는 등의 행동을 규격화합니다.

* 인터페이스 `IInteractable`을 선언하고, `void Interact();` 메서드를 정의하세요.
* 바닥에 떨어져 있는 **`DroppedAmmoBox`**(탄약 상자) 클래스와 **`Door`**(문) 클래스를 만들어 이 인터페이스를 구현하세요.
* `DroppedAmmoBox`의 `Interact()`: "탄약을 획득했습니다! (무기 장탄수 증가)" 출력
* `Door`의 `Interact()`: "철컥, 문이 열렸습니다." 출력



---

## 💻 학생이 구현해야 할 자식 클래스 구조 예시

* **`AssaultRifle` (자식 클래스):** `Firearm`을 상속받음. `Fire()` 호출 시 내부 중첩 클래스의 연사 모드를 확인하고 "타타탕! 돌격소총 3발 격발" 형태로 구현.
* **`Shotgun` (자식 클래스):** `Firearm`을 상속받음. `Fire()` 호출 시 "콰앙! 샷건 산탄 발사" 형태로 구현.

---

## 🚀 Main 함수 시뮬레이션 시나리오 (평가 기준)

학생은 `Main` 메서드에서 다음 시나리오가 부드럽게 작동하도록 다형성 배열을 제어해야 합니다.

```csharp
static void Main()
{
    // 1. 다형성 총기 배열 관리
    Firearm[] loadout = new Firearm[2];
    loadout[0] = new AssaultRifle("M4A1", 30);
    loadout[1] = new Shotgun("Remington", 8);

    // 일괄 사격 테스트 (오버라이딩 체감)
    foreach(var weapon in loadout) {
        weapon.Fire();
    }

    // 2. 인터페이스 배열을 통한 상호작용 (F키 누르기 시뮬레이션)
    IInteractable[] environment = new IInteractable[2];
    environment[0] = new Door();
    environment[1] = new DroppedAmmoBox();

    // 안전한 형변환(is, as) 복습 검증
    // 만약 상호작용 대상이 탄약 상자(DroppedAmmoBox)라면, 
    // 현재 들고 있는 loadout[0]의 탄약을 채워주는 로직을 연동해 보세요!
}

```
