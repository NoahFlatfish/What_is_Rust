# Rust의 기본 자료형 (Primitive Types) 📚

## 개요
프로그래밍의 기본이 되는 Rust의 기본 자료형들을 알아봅시다.

## 1. 숫자 타입

### 1.1 정수형 (정수: 소수점이 없는 숫자)
```rust
// 양수, 음수 모두 가능한 정수
let num1: i32 = -30;      // 가장 많이 사용! (-21억 ~ 21억)
let num2: i8 = -128;      // (-128 ~ 127)
let num3: i64 = -922337;  // 더 큰 범위

// 양수만 가능한 정수
let pos1: u32 = 30;       // 가장 많이 사용! (0 ~ 42억)
let pos2: u8 = 255;       // (0 ~ 255)
```

💡 **초보자 팁**: 
- 대부분의 경우 `i32` 사용
- 양수만 쓸 때는 `u32` 사용

### 1.2 실수형 (소수점이 있는 숫자)
```rust
let float1: f64 = 3.14159;  // 많이 사용! (더 정밀한 소수)
let float2: f32 = 3.14;     // (덜 정밀한 소수)

// 실생활 예시
let price: f64 = 29.99;     // 가격
let height: f64 = 175.5;    // 키
```

💡 **초보자 팁**: 
- 대부분 `f64` 사용
- 소수점 계산이 필요할 때 사용

## 2. 문자와 문자열

### 2.1 문자 (한 글자)
```rust
let letter: char = 'A';
let emoji: char = '😀';
let korean: char = '안';
let space: char = ' ';
```

### 2.2 문자열 (여러 글자)
```rust
// String 타입 (가장 많이 사용)
let name: String = String::from("Alice");
let greeting = "Hello".to_string();

// &str 타입 (문자열 참조)
let message: &str = "안녕하세요!";

// 문자열 합치기
let first = "Hello".to_string();
let second = "World".to_string();
let hello_world = first + &second;  // "HelloWorld"
```

💡 **초보자 팁**: 
- 일반적으로 `String` 사용
- 변하지 않는 텍스트는 `&str` 사용

## 3. 불리언 (참/거짓)
```rust
let is_rust_fun: bool = true;
let is_weekend = false;

// 실제 사용 예시
let is_adult = age >= 18;
let can_vote = is_adult && is_citizen;
```

## 4. 단위 타입
```rust
// 값이 없음을 표현
let empty: () = ();
```

## 자주 하는 형변환
```rust
// 숫자 -> 문자열
let age = 25;
let age_str = age.to_string();

// 문자열 -> 숫자
let price_str = "199";
let price_num = price_str.parse::<i32>().unwrap();

// 정수 -> 실수
let integer = 5;
let float = integer as f64;  // 5.0
```

## 초보자가 알아야 할 핵심 사항! 🎯

1. **가장 많이 쓰는 타입**:
   - 숫자: `i32`, `f64`
   - 문자열: `String`
   - 참/거짓: `bool`

2. **값 변경이 필요할 때**:
```rust
let mut score = 85;  // mut 키워드 사용
score = 90;  // 값 변경 가능
```

3. **타입 추론**:
```rust
let name = "Alice".to_string();  // 자동으로 String 타입으로 추론
let age = 30;                    // 자동으로 i32 타입으로 추론
```

## 자주하는 실수 ⚠️

1. 문자열 다루기
```rust
// 틀린 예
let s1: String = "hello";  // 컴파일 에러!

// 맞는 예
let s1: String = String::from("hello");
let s2: String = "hello".to_string();
```

2. 변수 변경하기
```rust
// 틀린 예
let x = 5;
x = 6;  // 에러! mut 키워드가 없음

// 맞는 예
let mut x = 5;
x = 6;  // OK!
```
