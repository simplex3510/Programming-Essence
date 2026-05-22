## 🎮 C# Instance vs Static 개념 강화 문제

### 1. 게임 서버 접속자 수 카운터 (static 변수 활용)

게임 서버에 접속하는 플레이어를 관리하는 User 클래스를 만드세요.

* **조건:**
* 각 유저 객체는 자신만의 username(인스턴스 변수)을 가집니다.
* 전체 서버에 접속 중인 총 유저 수를 나타내는 totalUsers(static 변수)를 만드세요.
* 생성자에서 유저가 한 명 생성될 때마다 totalUsers를 1씩 증가시키고, 현재 총 접속자 수를 출력하세요.
* **생각해볼 점:** totalUsers를 인스턴스 변수로 만들면 왜 총 접속자 수를 셀 수 없을까요?



### 2. 절대적인 게임 설정 값 관리 (static 클래스와 메서드)

게임 내에서 모든 캐릭터에게 공통으로 적용되는 중력 가속도와 물리 계산을 담당하는 GamePhysics 클래스를 만드세요.

* **조건:**
* GamePhysics 클래스는 객체를 생성할 수 없도록 static 클래스로 선언합니다.
* 상수로 사용할 중력 가속도 Gravity(static 변수, 값: $9.81$)를 선언하세요.
* 물체의 질량(double mass)을 매개변수로 받아 무게($mass \times Gravity$)를 반환하는 CalculateWeight(static 메서드)를 구현하세요.
* Main 메서드에서 new 키워드 없이 이 메서드를 바로 호출해 보세요.



### 3. 골드 수급과 누적 기부금 (Instance vs Static 비교)

길드 시스템을 구현하기 위해 GuildMember 클래스를 만드세요.

* **조건:**
* 각 길드원은 자신이 보유한 돈인 myGold(인스턴스 변수)를 가집니다.
* 길드 전체가 공유하는 자금인 guildFunds(static 변수)를 만드세요.
* Contribute(int amount) 메서드를 만드세요. 이 메서드가 호출되면 길드원의 myGold는 amount만큼 차감되고, guildFunds는 amount만큼 증가해야 합니다.
* 멤버 3명을 생성하여 각각 기부해보고, 개인 잔액과 길드 총자금의 변화를 확인하세요.



### 4. 몬스터 도감과 고유 인덱스 (static을 이용한 ID 발급)

소환되는 몬스터를 관리하는 Monster 클래스를 만드세요.

* **조건:**
* 몬스터가 생성될 때마다 1부터 시작하여 자동으로 고유한 번호가 부여되는 monsterId(인스턴스 변수)를 가집니다.
* 이를 구현하기 위해 다음 몬스터에게 부여할 번호를 기억하는 nextId(static 변수)를 활용하세요.
* 생성자에서 nextId를 monsterId에 대입한 후, nextId를 1 증가시킵니다.
* 몬스터를 3마리 생성하여 각 몬스터의 monsterId가 다르게 출력되는지 확인하세요.



### 5. 오류 찾기: 인스턴스 영역과 스태틱 영역의 경계

다음 C# 코드는 컴파일 에러가 발생합니다. **어느 라인에서 왜 에러가 발생하는지** 이유를 설명하고, 올바르게 수정하세요.

```csharp
class Character
{
    public string name = "전사";       // 인스턴스 변수
    public static int maxLevel = 100; // 스태틱 변수

    public static void ShowInfo()
    {
        // 아래 두 출력문 중 에러가 발생하는 곳은 어디일까요?
        Console.WriteLine($"최대 레벨: {maxLevel}");
        Console.WriteLine($"캐릭터 이름: {name}");
    }
}

```

* **핵심 질문:** static 메서드 안에서 일반 인스턴스 변수를 왜 곧바로 참조할 수 없을까요?
