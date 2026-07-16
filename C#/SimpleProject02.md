# 🎮 대규모 확장형 장비 및 아이템 시스템 아키텍처 설계 (FPS/RPG)

이 프로젝트는 새로운 총기나 아이템이 추가될 때 **기존 코드를 단 한 줄도 수정하지 않고(개방-폐쇄 원칙, OCP)** 확장할 수 있는 유연한 시스템을 설계하는 것이 목표입니다.

---

## 🏗️ 1. 핵심 아키텍처 및 클래스 관계도 (구조 설계)

학생이 이해하기 쉽도록 구조를 세 단계로 레이어링했습니다.

```
       [ IItem ] (최상위 규격: 인벤토리에 들어가는 모든 것)
          │
    ┌─────┴───────────────────────┐
 [ IEquipment ] (장착 가능한 것)  [ IUsable ] (일회성 소비템)
    │                             │
 [Abstract] BaseWeapon            └─ (포션, 탄약박스 등 무한 확장)
    │
    └─ (소총, 샷건, 저격총 등 무한 확장)

```

---

## 🛠️ 2. 과제 핵심 요구 사항 (구조적 설계 부문)

### ① 아이템 기본 계약 인터페이스: `IItem`

게임 내 모든 아이템(무기, 장비, 소비템, 퀘스트 아이템 등)의 범용 규격을 정의합니다.

* `string Id { get; }` (아이템 고유 식별자 - 향후 데이터베이스 연동용)
* `string Name { get; }` (인벤토리에 표시될 이름)
* `int Weight { get; }` (무게 제한 시스템용)

### ② 장비 및 슬롯 인터페이스: `IEquipment` (상속형 인터페이스)

`IItem`을 상속받아, 캐릭터의 장비 슬롯(무기 슬롯, 방어구 슬롯 등)에 "장착"할 수 있는 물건들의 공통 규격을 선언합니다.

* `void Equip();` (장착 시 실행할 로직 - 능력치 상승, 외형 적용 등)
* `void UnEquip();` (해제 시 실행할 로직)

---

### ③ 무기 시스템의 베이스 추상 클래스: `BaseWeapon`

`IItem`과 `IEquipment`를 모두 상속받는 **무기 계열의 공통 추상 클래스**입니다.
여기에 **중첩 클래스**를 활용해 복잡한 내부 구동 구조(사격 제어 장치)를 은닉합니다.

* **필드 및 프로퍼티:**
* `int CurrentAmmo` (현재 탄환)
* `int MaxAmmo` (최대 탄환)


* **일반 메서드:**
* `public void Reload()`: "장전 시작" 출력 후 `CurrentAmmo`를 최대치로 설정하는 공통 공정.


* **추상 메서드 (하위 무기가 직접 정의할 격발 규격):**
* `protected abstract void ExecuteFire();` (실제 총탄이 발사될 때의 고유 연출 및 피해량 처리)



```csharp
// 💡 중첩 클래스 (Nested Class) 활용: 총기 내부의 발사 트리거 메커니즘 은닉
public abstract class BaseWeapon : IEquipment
{
    // 외부 클래스(인벤토리, 플레이어 제어 등)에서는 이 복잡한 트리거 상태 구조를 알 필요가 없습니다.
    protected class TriggerGroup
    {
        public string FireModeName { get; set; } // "단발", "연사", "점사"
        public float FireRate { get; set; }      // 발사 속도 딜레이
        public int BurstCount { get; set; }     // 점사 시 격발 수
    }

    protected TriggerGroup weaponTrigger; // 내부용 트리거 인스턴스
}

```

---

### ④ 일회성 아이템 계약 인터페이스: `IUsable`

포션, 탄약 박스 등 "사용 후 소모되는" 아이템들의 계약입니다.

* `void Use(Player target);` (대상을 지정하여 소모성 효과 적용)

---

## 🚀 3. 학생이 직접 설계하고 증명해야 할 시나리오 (Main)

구체적인 무기 콘텐츠 클래스는 오직 **하나씩만** 만들어서 시스템이 잘 작동하는지 뼈대만 증명하도록 유도합니다.

```csharp
class Program
{
    static void Main()
    {
        // 1. 인벤토리 시스템 (IItem 규격을 따르는 모든 것을 담을 수 있는 가방)
        IItem[] inventory = new IItem[3];
        inventory[0] = new AssaultRifle("M4A1", 30);  // IEquipment -> IItem 상속 관계
        inventory[1] = new HealsPotion("구급상자");     // IUsable -> IItem 상속 관계
        inventory[2] = new DroppedAmmoBox("5.56mm 탄약박스");

        Console.WriteLine("=== [시스템 테스트 1: 인벤토리 일괄 목록 파악] ===");
        foreach (IItem item in inventory)
        {
            Console.WriteLine($"아이템 이름: {item.Name} | 무게: {item.Weight}kg");
        }

        Console.WriteLine("\n=== [시스템 테스트 2: 장비 장착 및 해제 테스트] ===");
        // safe-casting (as, is)을 활용하여 장비 타입만 골라내 장착/해제 테스트 진행
        foreach (IItem item in inventory)
        {
            if (item is IEquipment equipment)
            {
                equipment.Equip();
                
                // 무기인 경우 즉시 격발 테스트 연계
                if (equipment is BaseWeapon weapon)
                {
                    weapon.Reload();
                }
                
                equipment.UnEquip();
            }
        }

        Console.WriteLine("\n=== [시스템 테스트 3: 소비형 아이템 사용 테스트] ===");
        // 사용 가능(IUsable)한 아이템만 분류하여 작동
        Player dummyPlayer = new Player();
        foreach (IItem item in inventory)
        {
            if (item is IUsable usableItem)
            {
                usableItem.Use(dummyPlayer);
            }
        }
    }
}

```
