# Rust의 복합 자료형 (Compound Types) 📚

## 개요
여러 값을 하나로 묶어서 사용할 수 있는 Rust의 복합 자료형들을 알아봅시다.
기본 자료형들을 조합해서 더 복잡한 데이터를 표현할 수 있습니다!

## 1. 배열과 벡터 (여러 값을 순서대로 저장)

### 1.1 배열 (Array - 크기가 고정)
```rust
// 배열 선언 (타입과 크기를 지정해야 함)
let numbers: [i32; 5] = [1, 2, 3, 4, 5];
let grades = [85, 90, 95, 88, 92];  // 타입 추론

// 같은 값으로 배열 초기화
let zeros = [0; 5];  // [0, 0, 0, 0, 0]

// 배열의 값 접근
let first = numbers[0];  // 1
let second = numbers[1]; // 2
```

### 1.2 벡터 (Vector - 크기가 자유로움)
```rust
// 벡터 생성
let mut scores: Vec<i32> = vec![90, 85, 95];
let mut names: Vec<String> = Vec::new();  // 빈 벡터

// 벡터에 값 추가/삭제
scores.push(88);       // 끝에 추가
let last = scores.pop();  // 마지막 값 제거

// 벡터 값 접근
let first = &scores[0];
let maybe_second = scores.get(1);  // Option 타입 반환
```

💡 **초보자 팁**: 
- 개수가 변할 수 있는 목록은 `Vec` 사용
- 개수가 고정된 경우만 배열 사용

## 2. 튜플 (서로 다른 타입의 값들을 묶기)
```rust
// 튜플 생성
let person: (String, i32, bool) = ("Alice".to_string(), 30, true);
let point = (10, 20);  // 좌표

// 값 꺼내기
let name = person.0;    // "Alice"
let age = person.1;     // 30
let is_student = person.2;  // true

// 구조 분해
let (name, age, is_student) = person;
let (x, y) = point;
```

## 3. 구조체 (관련 데이터를 하나로 묶기)

### 3.1 일반 구조체
```rust
// 구조체 정의
struct Person {
    name: String,
    age: i32,
    is_student: bool,
}

// 구조체 사용
let alice = Person {
    name: String::from("Alice"),
    age: 30,
    is_student: true,
};

// 값 접근
println!("이름: {}", alice.name);
println!("나이: {}", alice.age);
```

### 3.2 튜플 구조체
```rust
struct Point(i32, i32);
struct Color(u8, u8, u8);  // RGB

let origin = Point(0, 0);
let black = Color(0, 0, 0);
```

## 4. 열거형 (Enum - 여러 가능성 중 하나를 표현)
```rust
// 열거형 정의
enum Status {
    Active,
    Inactive,
    Pending,
}

enum Message {
    Quit,
    Move { x: i32, y: i32 },
    Write(String),
    ChangeColor(i32, i32, i32),
}

// 사용 예시
let status = Status::Active;

let message = Message::Write(String::from("안녕하세요"));
```

## 5. Option과 Result (특별한 열거형)

### 5.1 Option (값이 있거나 없을 때)
```rust
// Option 사용
let some_number: Option<i32> = Some(5);
let no_number: Option<i32> = None;

// 값 사용하기
match some_number {
    Some(n) => println!("숫자: {}", n),
    None => println!("값이 없습니다"),
}
```

### 5.2 Result (성공 또는 실패를 나타낼 때)
```rust
// Result 사용
fn divide(a: i32, b: i32) -> Result<i32, String> {
    if b == 0 {
        Err("0으로 나눌 수 없습니다".to_string())
    } else {
        Ok(a / b)
    }
}

// 결과 처리
match divide(10, 2) {
    Ok(result) => println!("결과: {}", result),
    Err(e) => println!("에러: {}", e),
}
```

## 초보자를 위한 핵심 포인트! 🎯

1. **자주 사용하는 조합**:
```rust
// 벡터 안의 구조체
let mut users: Vec<Person> = Vec::new();
users.push(Person { name: "Alice".to_string(), age: 30, is_student: true });

// Option 벡터
let numbers: Vec<Option<i32>> = vec![Some(1), None, Some(3)];
```

2. **컬렉션 선택 가이드**:
- 크기가 변하는 목록 → `Vec<T>`
- 관련 데이터 묶기 → `struct`
- 여러 가능성 중 하나 → `enum`
- 실패할 수 있는 작업 → `Result`
- 없을 수 있는 값 → `Option`

3. **메서드 정의**:
```rust
impl Person {
    fn new(name: String, age: i32) -> Person {
        Person {
            name,
            age,
            is_student: false,
        }
    }

    fn introduce(&self) {
        println!("안녕하세요, {}입니다!", self.name);
    }
}
```

## 자주하는 실수 ⚠️

1. 벡터 접근
```rust
// 틀린 예
let vec = vec![1, 2, 3];
let value = vec[5];  // 패닉! 인덱스가 범위를 벗어남

// 안전한 예
if let Some(value) = vec.get(5) {
    println!("값: {}", value);
} else {
    println!("인덱스가 범위를 벗어났습니다");
}
```

2. Option 값 사용
```rust
// 틀린 예
let opt: Option<i32> = Some(5);
let value = opt;  // Option을 직접 사용할 수 없음

// 맞는 예
if let Some(value) = opt {
    println!("값: {}", value);
}
```
