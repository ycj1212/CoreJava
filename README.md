# **CoreJava**

---
## **5. 상속 (Inheritance)**

4장에서 클래스와 오브젝트를 소개했다.
이 장에서 당신은 상속에 대하여 학습할 것이고, 객체지향프로그래밍의 또 다른 핵심적인 개념이다.
상속의 개념은 당신이 존재하는 클래스에 의거하여? 새로운 클래스를 생성할 수 있다.
너가 존재하는 클래스로부터 상속받을 때, 당신은 그것의 메소드를 재사용하고, 당신은  새로운 메소드와 새로운 환경에서 새로운 클래스에 적용된 필드를 추가할 수 있다.
이 기술은 자바 프로그래밍에서 필수적이다.

이 장은 또한 reflection(실행중인 프로그램에서 클래스와 그들의 properties에 대하여 더 알아보는 능력)을 포함한다. Reflection은 강력한 특징이나, 확실히 복잡하다.
reflection이 application프로그래머보다 tool개발자들에게 흥미가 더 큰 이후로, 당신은 아마도 처음 읽었을 때 그 부분을 훑어보고 나중에 다시 볼 수 있을 것이다.

- 5-1 클래스, 부모클래스(Superclass), 자식클래스(Subclass)
    우리가 이전 장에서 다루던 Employee 클래스를 돌아보자.
    당신이 관리자(manager)가 다른 직원(employee)으로 부터 따로 다룬 회사에서 일을 한다고 가정하자.
    물론 관리자는 많은 면에서 마치 직원과 같다.
    직원과 관리자 둘 다 봉급을 받는다.
    그러나 직원이 그들의 봉급을 받는 대가로 할당된 일들을 끝내는 것을 예상되는 반면, 관리자는 만약 그들이 실제로 그들이 하기로 되어있던 것을 달성한다면 bonuses를 받는다.
    이것은 상속을 절실히 바라는 환경의 종류이다.
    왜? 음, 너는 새로운 클래스, Manager, 추가기능을 정의하는 것을 필요로 한다.
    그러나 당신은 Employee클래스에서 이미 프로그램했었던 것들의 일부를 보유?할 수 있다. 그리고 original 클래스의 모든 필드가 보존될 수 있다.
    더 추상적으로, 명백한 Manager와 Employee 사이에 명백한 "is-a" 관계가 있다.
    모든 manager은 하나의 employee : 이 "is-a" 관계는 상속의 특징이다.

    ```
    필기 : 이 장에서, 우리는 employees와 managers 전형적인 예시를 사용하나, 우리는 당신에게 이 예를 에누리하여 들어줄 것을 요청해야 한다.
    현실세계에서 직원은 관리자가 될 수 있다. 그래서 당신은 직원의 한 역할로서 관리자가 되는 모델을 원할것이다. 하나의 자식클래스가 아니라.
    그러나, 우리의 예시에서 우리는 두 종류의 사람에 의해 설립된 기업?법인?세계를 추정한다:영원히 직원인 사람들, 그리고 항상 관리자가 될 지도 모르는 사람들
    ```

    - 5-1-1 자식클래스 정의
        당신이 Employee클래스로부터 상속받은 Manager클래스를 정의하는 방법이 있다.
        상속을 의미하는 *extends* 자바 키워드를 사용해라.
        
        ```
        public class Manager extends Employee
        {
            // added methods and fields
        }
        ```
        
        ```
        C++ 필기 : 상속은 자바와 C++에서 비슷하다.
        자바는 : 토큰 대신에 extends 키워드를 사용한다.
        자바에서 모든 상속은 public 상속이다; private과 protected 상속의 C++특징에서 유사성이 없다.
        ```

        extends 키워드는 당신이 existing 클래스에서 파생된 새로운 클래스를 생성한다는 것을 나타낸다.
        existing 클래스는 superclass, base class, parent class 라고 불린다.
        새로운 클래스는 subclass, derived class, child class 라고 불린다.
        슈퍼클래스와 서브클래스의 표현?용어?는 자바 프로그래머에 의해 가장 흔히 사용된다, 비록 몇몇 프로그래머들이 부모/자식 유사성?유추?을 선호하지만,
        이것은 또한 "상속" 주제와 함께 병행한다.

        Employee 클래스는 슈퍼클래스이다. 그러나, 그것이 서브클래스보다 우월하기 때문에 또는 더 많은 기능을 포함하고 있기 때문은 아니다.
        사실, 그 반대는 사실이다 : 서브클래스는 슈퍼클래스보다 더 많은 기능을 가지고 있다.
        예를 들면, 우리가 Manager클래스 코드의 나머지 부분을 살펴보면 알 수 있듯이, Manager 클래스는 슈퍼클래스 Employee 보다 더 많은 정보를 요약화하고, 더 많은 기능을 가진다.

        ```
        필기 : 접두사 super와 sub는 이론상으로 컴퓨터 과학과 수학에서 사용되는 집합의 언어로부터 유래한다.
        모든 employees 집합은 모든 managers 집합을 포함하므로, managers 집합의 superset 이라고 한다.
        또는, 다르게 말하면, 모든 managers 집합은 모든 employees 집합의 subset 이다.
        ```

        우리의 Manager 클래스는 bonus를 저장하는 새로운 필드를 가지고 있고, 이것을 설정하는 새로운 메소드를 가지고 있다.

        ```
        public class Manager extends Employee
        {
            private double bonus;
            ...
            public void setBonus(double bonus)
            {
                this.bonus = bonus;
            }
        }
        ```

        이 메소드와 필드에 대하여 특별한 것이 없다.
        만약 당신이 Manager 객체를 가지고 있다면, 당신은 간단하게 setBonus 메소드를 적용할 수 있다.

        ```
        Manager boss = ...;
        boss.setBonus(5000);
        ```

        물론, 만약 당신이 Employee 객체를 가지고 있다면, 당신은 setBonus 메소드를 적용할 수 없다. - Employee 클래스에서 정의된 메소드가 아니다.

        그러나 당신은 Manager객체의 getName, getHireDay 와 같은 메소드를 사용할 수 있다.
        비록 이 메소드들이 Manager클래스에서 명확하게 정의되지 않았더라도, Employee 슈퍼클래스로부터 자동적으로 상속받을 수 있다.

        비슷하게, name, salary, hireDay 필드들은 슈퍼클래스로부터 가져온다.
        모든 Manager 객체가 name, salary, hrieDay, bonus 필드를 가지고 있다.

        상속받은 슈퍼클래스에 의해 서브클래스를 정의할 때, 당신은 오직 서브클래스와 슈퍼클래스 사이의 차이점을 나타내는 것을 필요로 한다.
        클래스를 설계할 때, 당신은 슈퍼클래스에서 가장 일반적인 메소드를 사용하고, 서브클래스에서 더 전문적인 메소드를 사용한다.
        //
        공통의?흔한? 기능을 슈퍼클래스로 옮기는 것에 의해 제외하는 것은 객체지향 프로그래밍에서 흔히 볼 수 있다.
        슈퍼 클래스로 옮겨서 공통의 기능을 알아내는 것은 객체 지향 프로그래밍에서 흔히 볼 수 있다.
        //

    - 5-1-2 메소드 오버라이딩
        슈퍼클래스 메소드의 몇몇은 Manager 서브클래스에 적절하지 않다.
        특히, getSalary 메소드는 base salary와 bonus의 합계를 반환하여야한다.
        당신은 슈퍼클래스 메소드를 오버라이드 한 새로운 메소드를 제공하는것을 필요로 한다.
        
        ```
        public class Manager extends Employee
        {
            ...
            public double getSalary()
            {
                ...
            }
            ...
        }
        ```

        당신은 어떻게 이 메소드를 구현할 수 있나요?
        언뜻 보기에는 간단하게 될 것 같다. - 단지 salary와 bonus 필드의 합계를 반환해라.

        ```
        public double getSalary()
        {
            return salary + bonus;  // won't work
        }
        ```
        
        하지만, 작동하지 않을 것이다.
        오직 Employee메소드가 Employee클래스의 private필드에 집적 접근하는 것을 recall해라.
        이것은 Manager클래스의 getSalary메소드가 salary필드에 직접 접근할 수 없다는 것을 의미한다.
        만약 Manager메소드가 그들의 private필드에 접근하는 것을 원한다면, 그들은 모든 다른 메소드를 사용하는 것을 해야한다. - public 인터페이스를 사용해라, 이 경우에 있어서 Employee클래스의 public getSalary메소드 // ???

        다시 시도해보자. 당신은 salary 필드에 간단하게 접근하는 것 대신에 getSalary를 호출하는 것을 필요로 한다 :
        
        ```
        public double getSalary()
        {
            double baseSalary = getSalary();    // still won't work
            return baseSalary + bonus;
        }
        ```
        
        그 문제는 getSalary를 호출하는 것이 간단하게 스스로를 호출한다는 것이다, 왜냐하면 Manager클래스가 getSalary메소드(다시 말해, 그 우리가 구현하고자 하는 메소드)를 가지고 있기 때문이다.
        그 결과는 같은 메소드를 호출하는 것의 무한한 chain이고, 프로그램 충돌로 이어진다.

        우리는 우리가 current클래스가 아닌, Employee슈퍼클래스의 getSalary메소드 호출을 원하는 것을 나타내는 것을 필요로 한다.
        당신은 이 목적을 위해 특별한 키워드 super을 사용한다.

        `super.getSalary()`은 Employee클래스의 getSalary메소드를 호출한다.
        Manager클래스를 위한 getSalary메소드의 옳은 버전이 있다. :
        
        ```
        public double getSalary()
        {
            double baseSalary = super.getSalary();
            return baseSalary + bonus;
        }
        ```

        ```
        필기 : 몇몇의 사람들은 super을 this참조와 비슷하다고 생각한다.
        그러나 그 유추는 꽤 정확하지 않다 : super은 객체의 참조가 아니다.
        예를 들면, 당신은 또 다른 object변수에 super값을 할당할 수 없다.
        대신에, super는 슈퍼클래스 메소드를 불러오는 컴파일러로 향하는 특별한 키워드이다.
        ```

        당신도 봤었듯이, 서브클래스는 필드를 추가할 수 있고, 메소드를 추가할 수 있거나, 슈퍼클래스의 메소드를 오버라이드 할 수 있다.
        그러나, 상속은 결코 어느 필드나 메소드를 떠날 수 없다.
        
        ```
        C++ 필기 : 자바는 슈퍼클래스 메소드를 호출하기 위해 super키워드를 사용한다.
        C++에서, 대신에 당신은 :: 연산자와 함께 슈퍼클래스의 이름을 사용할 것이다.
        예를 들면, Manager클래스의 getSalary메소드는 super.getSalary 대신에 Employee::getSalary를 호출할 것이다.
        ```

    - 5-1-3 서브클래스 생성자
        우리의 예시를 완료하는 것은, 생성자를 제공하라고 시킨다.
        
        ```
        public Manager(String name, double salary, int year, int month, int day)
        {
            super(name, salary, year, month, day);
            bonus = 0;
        }
        ```
        
        여기, super키워드는 다른 의미를 가지고 있다.
        이 지시
        `super(n, s, year, month, day);`
        는 "Employee슈퍼클래스의 생성자를 n, s, year, month, day와 같은 매개변수와 함께 호출해라" 의 약칭이다.
        Manager생성자가 Employee클래스의 private필드에 접근할 수 없을 때 부터, 생성자를 통해 그들을 초기화 해야한다.
        생성자는 특별한 super문법에서 호출된다.
        super을 사용하는 호출은 서브클래스의 생성자에서 첫 문장이 되어야한다.
        만약 서브클래스 생성자가 슈퍼클래스 생성자를 명확하게 호출하지 않는다면, 슈퍼클래스의 no-argument생성자가 호출된다.
        만약 슈퍼클래스가 no-argument생성자를 가지고 있지 않다면 그리고 서브클래스 생성자가 또 다른 슈퍼클래스 생성자를 명확하게 호출하지 않는다면, 자바 컴파일러는 에러를 제출한다.

        ```
        필기 : this 키워드가 두가지 의미를 가지고 있다는 것을 회상해라 : 명백한 매개변수의 참조를 의미하는 것과 같은 클래스의 또 다른 생성자를 호출하는 것.
        마찬가지로, super키워드는 두가지 의미를 가진다 : 슈퍼클래스 메소드를 호출하는 것과 슈퍼클래스 생성자를 호출하는 것.
        생성자를 호출하곤 했을 때, this와 super키워드는 면밀히 관련이 있다.
        생성자 호출은 오직 또 다른 생성자에서 첫 문장으로서 발생할 수 있다.
        생성자 매개변수는 같은 클래스(this)나 슈퍼클래스(super)의 또 다른 생성자를 넘겨받는다. 
        ```

        ```
        C++ 필기 : C++ 생성자에서, 당신은 super을 호출하지 않지만, 슈퍼클래스 생성자에서 initializer list 문법을 사용한다.
        C++에서 Manager생성자는 이와 같이 본다.
            
            Manager::Manager(String name, double salary, int year, int month, int day)  // c++
            : Employee(name, salary, year, month, day)
            {
                bonus = 0;
            }
        ```
        
        당신이 Manager객체에 getSalary메소드를 재정의한 후, managers는 자동적으로 그들의 salaries를 더한 bonus를 가지게 될 것이다.
        작업에서 이런 예시가 있다.
        우리는 새로운 manager를 만들고, manager의 bonus를 설정한다.

        ```
        Manager boss = new Manager("Carl Cracker", 80000, 1987, 12, 15);
        boss.setBonus(5000);
        ```

        우리는 세 개의 employee의 배열을 만든다. 

        `Employee[] staff = new Employee[3];`

        