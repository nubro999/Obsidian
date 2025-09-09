

|키워드|역할/의미|
|---|---|
|fn|함수 정의|
|struct|구조체 정의|
|enum|열거형 정의|
|impl|메서드 구현|
|trait|인터페이스(함수 집합) 정의|
|let, mut|변수 선언, 변경 가능 표시|
|const, static|상수, 전역 변수|
|match|패턴 매칭|
|if, else|조건문|
|for, while, loop|반복문|
|ref, &, *|참조, 역참조|
|as|형변환|
|crate, extern|외부 라이브러리, 패키지|
|Self, self, super|타입, 모듈 참조|

impl, trait 구현예시

```Rust
trait Drawable {
    fn draw(&self);
}

struct Circle;
struct Square;

impl Drawable for Circle {
    fn draw(&self) {
        println!("Drawing a Circle!");
    }
}

impl Drawable for Square {
    fn draw(&self) {
        println!("Drawing a Square!");
    }
}

fn draw_shape(shape: &dyn Drawable) {
    shape.draw();
}

fn main() {
    let c = Circle;
    let s = Square;

    draw_shape(&c); // Drawing a Circle!
    draw_shape(&s); // Drawing a Square!
}
```

anchor 셋팅은 홈페이지 따라서 하자 왜 우크라이나로 라우팅되는겨