## 5차시 상속

## 상속의 필요성

- 기능 확장을 하거나 기존 클래스를 기반으로 클래스를 만들 때 같은 소스를 계속해서 나눠서 사용한다면 수정에 시간이 걸리고, 소스 파악이나 관리가 어려워지고, 유지보수도 어려워짐
- 상속을 사용하자!

### 상속의 구조와 기본 개념

<img width="198" alt="Image" src="https://github.com/user-attachments/assets/3d434039-a41a-40ce-9a33-cf9f77af7a78" />

- **화살표가 부모**임
- 부모의 **private**을 제외한 모든 것은 자식에게 **상속**됨.
- 부모의 메서드를 자식이 재정의하는 것을 **Override**라고 함

### 다중상속에 대해서

- **다중 상속은 Java에서는 금지!!!**
    - C++에서는 됨.
    - 만약 한다면 `클래스이름::메서드이름` 형식으로 어떤 클래스의 메서드를 사용하는지를 명시해야됨

<img width="259" alt="Image" src="https://github.com/user-attachments/assets/54de6929-55c4-4791-ad24-5e8ee3eab2bb" />

- `ComboDrive`에서 `burn()`을 사용할 때 누구의 burn인지가 모호함 → **금지 이유**
- C#는 재정의 할 경우 `override` 키워드를 작성해야됨.

    ```csharp
    // C# 예시
    class Parent {
        public virtual void Method() { Console.WriteLine("Parent"); }
    }
    
    class Child : Parent {
        public override void Method() { Console.WriteLine("Child"); }
    }
    ```

- 부모의 기능을 사용하고 싶을 때
    - Java: `super`, C#: `Base,` C++: `_super`

### 상속 주의점

- final이 붙은 클래스는 상속 안되며, final 메서드도 재정의 안됨
    - 예: String은 상속 안됨

      <img width="476" alt="Image" src="https://github.com/user-attachments/assets/1bfc0242-f77a-49a7-9f3c-844eaaf21edc" />

- 상속받을 때 부모클래스의 생성자를 충족시키는 자식 클래스 생성자를 만들어야함
    - 즉, 부모클래스의 생성자를 `super()` 로 호출해야됨.

    ```csharp
    public SuperHero(String name, int hp) {
            super(name, hp);
        }
    ```

    - 혹은 부모클래스의 기본 생성자를 만들어야됨.
        - 이거는 비추천!

          → 상속 자체가 부모클래스에서 기능을 확장하는것인데, 이것때문에 부모클래스에 새롭게 추가를 하니까

- 생성자 동작
    - 모든 생성자는, **“부모 인스턴스의 생성자"**를 먼저 호출
    - 생성자의 선두에 `super()` 가 없으면, 암묵적인 `super()` 가 추가 됨
- 올바른 상속 구별
    - **자식 is-a 부모** 원칙이라는 규칙을 대입하자
    - SuperHero is a Hero
- 잘못된 상속 예시

<img width="652" alt="Image" src="https://github.com/user-attachments/assets/fc6cb7af-a2eb-4d10-ad73-d4223f2b94de" />

    - 클래스를 확장할 때 현실세계와의 모순이 생긴다?
    - 객체 지향의 3대 특징 중 1가지 **“다형성"**을 이용할 수 없게 된다
    - 포션은 무기가 아니다. **개념적으로 잘못된 상속**

- 부모클래스라면 **추상적**이고, 자식클래스라면 **더 구체적**이게 됨