# 🐍 Python 딕셔너리 & 세트 마스터: 개념·논리 강화 중상급 15선

### [문제 1] [딕셔너리] get() 메서드를 활용한 안전한 기본값 처리

딕셔너리에서 존재하지 않는 키를 대괄호(`[]`)로 접근하면 `KeyError`가 발생합니다. `get()` 메서드를 활용하여, `user_profile`에 `'country'`라는 키가 있으면 그 값을 가져오고, **없으면 기본값으로 `'Unknown'`을 안전하게 반환**하도록 빈칸을 완성하세요.

```python
user_profile = {'name': 'Alex', 'age': 28, 'role': 'Data Analyst'}

# 'country' 키가 없으면 'Unknown'을 반환하도록 설정
country_info = user_profile.________(________)

print(country_info)
# 출력 예시: Unknown

```

---

### [문제 2] [딕셔너리] setdefault()를 이용한 카운팅(Counting) 논리

텍스트 데이터에서 각 알파벳이 몇 번 등장하는지 세려고 합니다. `setdefault()` 메서드는 키가 존재하지 않을 때만 기본값을 설정해 주는 특징이 있습니다. 이를 활용하여 글자 수를 누적하는 반복문 빈칸을 완성하세요.

```python
text = "banana"
counter = {}

for char in text:
    # 키가 없으면 기본값 0을 세팅하고, 있으면 기존 값에 1을 더하는 한 줄 코드
    counter[char] = counter.________(char, 0) + 1

print(counter)
# 출력 예시: {'b': 1, 'a': 3, 'n': 2}

```

---

### [문제 3] [딕셔너리] 가변 객체(Mutable)의 키 지정 제약 이해

파이썬 딕셔너리의 키(Key)는 내부적으로 해시(Hash) 연산을 거치기 때문에 값이 변하지 않는 객체(Immutable)만 올 수 있습니다. 다음 코드에서 **오류(`TypeError`)가 발생하는 원인이 되는 키 유형**을 골라 기호를 적으세요.

```python
# 아래 중 에러를 유발하는 잘못된 딕셔너리 정의는 무엇일까요?
case_A = { (1, 2): "Coordinate" }
case_B = { [1, 2]: "Coordinates List" }
case_C = { "location": [10, 20] }

# 정답: ________

```

---

### [문제 4] [딕셔너리] update() 메서드를 통한 데이터 병합

기존 회원 정보 리스트인 `current_user`에 새로운 변경 사항이 담긴 `new_data`를 합쳐서 정보를 최신화(업데이트)하려고 합니다. 겹치는 키는 새로운 값으로 덮어씌우고, 새로운 키는 추가해 주는 메서드를 활용하여 빈칸을 채우세요.

```python
current_user = {'id': 'user77', 'level': 5, 'status': 'active'}
new_data = {'level': 6, 'last_login': '2026-07-18'}

# current_user 리스트에 new_data의 내용을 병합하세요.
current_user.________(________)

print(current_user)
# 출력 예시: {'id': 'user77', 'level': 6, 'status': 'active', 'last_login': '2026-07-18'}

```

---

### [문제 5] [딕셔너리] 딕셔너리 컴프리헨션(Dictionary Comprehension)

이름이 키로, 점수가 값으로 매칭된 `scores` 딕셔너리가 있습니다. 이 중 **점수가 80점 이상인 사람만 골라내어** 새로운 딕셔너리 `passed`를 만드는 컴프리헨션 코드를 완성하세요.

```python
scores = {'Kim': 75, 'Lee': 90, 'Park': 85, 'Choi': 60}

# 80점 이상인 사람만 필터링하는 딕셔너리 컴프리헨션을 작성하세요.
passed = {________ for k, v in scores.items() if ________}

print(passed)
# 출력 예시: {'Lee': 90, 'Park': 85}

```

---

### [문제 6] [딕셔너리] 키와 값의 위치 뒤집기 (Inverting)

딕셔너리의 Key와 Value의 역할을 서로 맞바꾼 새로운 딕셔너리 `inverted_dict`를 만들려고 합니다. 딕셔너리 컴프리헨션의 원리를 활용하여 빈칸을 완성하세요.

```python
original = {'A': 1, 'B': 2, 'C': 3}

# Key와 Value의 위치를 뒤집는 한 줄 코드를 작성하세요.
inverted_dict = {________ for ________ in original.items()}

print(inverted_dict)
# 출력 예시: {1: 'A', 2: 'B', 3: 'C'}

```

---

### [문제 7] [세트] 중복 원소 제거와 순서 보존의 한계 이해

세트(Set)는 중복을 허용하지 않는 아주 유용한 자료형입니다. 아래 정수 리스트에서 중복을 제거한 유일한 값들만 남기려고 합니다. 빈칸에 알맞은 형변환 코드를 작성하세요.

```python
raw_numbers = [3, 1, 2, 3, 4, 1, 2, 5]

# 중복을 제거하기 위해 리스트를 세트로 변환했다가 다시 리스트로 만드세요.
unique_numbers = list(________(raw_numbers))

print(unique_numbers)
# 출력 예시: [1, 2, 3, 4, 5] (주의: 세트는 순서가 없으므로 정렬 상태는 바뀔 수 있습니다)

```

---

### [문제 8] [세트] 빈 세트(Empty Set) 생성 시의 문법적 주의사항

파이썬에서 빈 딕셔너리는 `empty_dict = {}`로 간단히 만들 수 있습니다. 그렇다면 원소가 하나도 없는 빈 세트(Set)를 선언할 때 사용하는 올바른 구문을 빈칸에 채우세요.

```python
# 빈 세트를 선언하는 올바른 구문을 적으세요.
empty_set = ________

print(type(empty_set))
# 출력 예시: <class 'set'>

```

---

### [문제 9] [세트] add()와 update() 메서드의 데이터 추가 방식 차이

세트에 단일 원소를 추가할 때와 여러 개의 원소를 한 번에 풀어서 추가할 때 사용하는 메서드가 다릅니다. 출력 예시를 보고 빈칸에 알맞은 메서드를 배치하세요.

```python
my_set = {1, 2, 3}

# 1. 숫자 4를 단일 원소로 추가하기
my_set.________(4)

# 2. 리스트 [5, 6] 안의 원소들을 한꺼번에 풀어서 세트에 추가하기
my_set.________([5, 6])

print(my_set)
# 출력 예시: {1, 2, 3, 4, 5, 6}

```

---

### [문제 10] [세트] 교집합, 합집합, 차집합 연산자 활용

두 반의 동아리 활동 참여 명단 세트가 주어졌습니다. 두 동아리에 모두 참여하고 있는 학생(교집합)과 A 동아리에만 참여하고 있는 학생(차집합)을 구하는 빈칸을 연산자 기호로 채우세요.

```python
club_A = {'Kim', 'Lee', 'Park'}
club_B = {'Lee', 'Choi', 'Kim'}

# 1. 교집합 구하기 (두 곳 모두 속한 학생)
both_clubs = club_A ________ club_B

# 2. 차집합 구하기 (club_A에만 속한 학생)
only_A = club_A ________ club_B

print(both_clubs)  # 출력 예시: {'Kim', 'Lee'} (순서 무관)
print(only_A)      # 출력 예시: {'Park'}

```

---

### [문제 11] [세트] 대칭차집합(Symmetric Difference)을 이용한 고유 원소 추출

대칭차집합은 두 집합 중 **한 곳에만 속해 있고 공통되지 않은 원소들의 집합**을 의미합니다. 대칭차집합을 뜻하는 연산자 기호를 빈칸에 채워 넣으세요.

```python
set_X = {1, 2, 3, 4}
set_Y = {3, 4, 5, 6}

# 공통 원소 {3, 4}를 제외한 {1, 2, 5, 6}만 추출하기
unique_elements = set_X ________ set_Y

print(unique_elements)
# 출력 예시: {1, 2, 5, 6} (순서 무관)

```

---

### [문제 12] [세트] 세트 컴프리헨션(Set Comprehension)

1부터 10까지의 숫자 중에서 **홀수들의 제곱값**만을 모아 중복 없이 저장하는 세트를 만들려고 합니다. 세트 컴프리헨션을 활용하여 한 줄 코드를 완성하세요.

```python
# 1~10 사이의 홀수를 제곱한 값들로 세트를 구성하세요.
odd_squares = {________ for x in range(1, 11) if ________}

print(odd_squares)
# 출력 예시: {1, 9, 25, 49, 81} (순서 무관)

```

---

### [문제 13] [세트] remove()와 discard()의 안정성 차이

세트에서 요소를 지울 때, 해당 요소가 존재하지 않으면 에러를 내는 메서드가 있고, 에러 없이 안전하게 넘어가는 메서드가 있습니다. 빈칸에 알맞은 메서드 이름을 채우세요.

```python
programming_languages = {'Python', 'Java', 'C'}

# 'C++'는 리스트에 없습니다. 
# 에러(KeyError)를 발생시키지 않고 안전하게 무시하며 요소를 지우는 메서드를 쓰세요.
programming_languages.________('C++')

print(programming_languages)
# 출력 예시: {'Python', 'Java', 'C'} (에러 없이 그대로 유지)

```

---

### [문제 14] [종합] 두 리스트의 공통 요소 찾기 (해시 효율성 극대화)

두 개의 거대한 리스트에서 공통으로 존재하는 원소를 찾아내려고 합니다. `for`문을 중첩하면 성능이 매우 떨어지지만, **한쪽 리스트를 세트로 변환한 뒤 교집합 연산**을 수행하면 대단히 빠르게 해결할 수 있습니다. 이 논리를 코드로 구현하세요.

```python
large_list_A = [10, 20, 30, 40, 50, 60]
large_list_B = [40, 50, 60, 70, 80, 90]

# 세트 변환 및 교집합 연산을 이용하여 공통 요소를 구한 뒤, 다시 리스트로 변환하세요.
common_elements = 

print(sorted(common_elements))
# 출력 예시: [40, 50, 60]

```

---

### [문제 15] [종합] 딕셔너리와 세트를 결합한 카테고리별 유일값 관리

쇼핑몰의 구매 로그 데이터가 `(카테고리, 상품명)` 튜플 리스트로 주어집니다. 각 카테고리별로 **어떤 종류의 상품들이 구매되었는지 중복을 제거하고 기록**하려고 합니다. 딕셔너리의 value 공간을 세트(set)로 활용하여 데이터를 분류하는 코드를 완성하세요.

```python
purchase_logs = [
    ('Fashion', 'Shirts'),
    ('Electronics', 'Laptop'),
    ('Fashion', 'Shirts'),  # 중복 데이터
    ('Electronics', 'Mouse'),
    ('Fashion', 'Pants')
]

category_map = {}

for category, items in purchase_logs:
    # 1. category_map에 카테고리 키가 없다면 빈 세트(set())를 기본값으로 생성
    category_map.setdefault(category, ________)
    
    # 2. 해당 카테고리의 세트에 상품명(items)을 추가
    category_map[category].________(items)

print(category_map)
# 출력 예시: {'Fashion': {'Shirts', 'Pants'}, 'Electronics': {'Laptop', 'Mouse'}}

```
