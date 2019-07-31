# **CoreJava**

## **5. 상속 (Inheritance)**

4장에서 클래스와 오브젝트를 소개했다.
이 장에서 당신은 상속에 대하여 학습할 것이고, 객체지향프로그래밍의 또 다른 핵심적인 개념이다.
상속의 개념은 당신이 기본 클래스에 의거하여 새로운 클래스를 생성할 수 있다.
당신이 기본 클래스로부터 상속 받을 때, 당신은 그것의 메소드를 재사용하고, 새로운 환경에서 새로운 클래스에 적용된 새로운 메소드와 필드를 추가할 수 있다.
이 기술은 자바 프로그래밍에서 필수적이다.

이 장은 또한 리플렉션(reflection, 실행중인 프로그램에서 클래스와 그들의 속성?(properties)에 대하여 더 알아보는 능력)을 포함한다. 리플렉션은 강력한 특징이나, 확실히 복잡하다.
리플렉션이 응용 프로그래머보다 도구 개발자들에게 흥미가 더 큰 이후로, 당신은 아마도 처음 읽었을 때 그 부분을 훑어보고 나중에 다시 볼 수 있을 것이다.

### **5-1. 클래스, 슈퍼클래스(Superclass), 서브클래스(Subclass)**
   
우리가 이전 장에서 다루던 Employee 클래스를 돌아보자.
당신이 관리자(manager)가 다른 직원(employee)들과 다르게 대우받는 회사에서 일을 한다고 가정하자.
물론 관리자는 많은 면에서 마치 직원과 같다.
직원과 관리자 둘 다 봉급을 받는다.
그러나 직원이 봉급을 받는 대가로 할당된 일들을 끝내는 것이 예상되는 반면, 관리자는 만약 실제로 그들이 하기로 되어있던 것을 달성한다면 보너스를 받는다.
이것은 상속을 절실히 바라는 환경의 종류이다.
왜? 음, 당신은 새로운 클래스 *Manager* 를 정의하고 기능을 추가하는 것을 필요로 한다.
그러나 당신은 *Employee* 클래스에서 이미 프로그램했었던 것들의 일부를 유지할 수 있고, 최초(original) 클래스의 모든 필드가 보존될 수 있다.
더 추상적으로, *Manager* 와 *Employee* 사이에 분명한 "is-a" 관계가 있다.
모든 manager는 한 employee 이다 : 이 "is-a" 관계는 상속의 특징이다.

```
필기 : 이 장에서, 우리는 employees와 managers 전형적인 예시를 사용하나, 우리는 당신에게 이 예를 가감(에누리)하여 들어줄 것을 요청할 필요가 있다.
현실세계에서 직원은 관리자가 될 수 있어서, 당신은 직원의 한 역할로서 관리자가 되는 모델을 원할 것 이다, 하나의 서브 클래스가 아니라.
그러나, 이 예시에서 우리는 법인 세계가 두 종류의 사람에 의해 설립된 것이라고 추정한다 : 영원히 직원인 사람들, 그리고 항상 관리자였던 사람들.
```

#### **5-1-1 서브클래스 정의**

당신이 *Employee* 클래스로부터 상속받은 *Manager* 클래스를 정의하는 방법이 있다.
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
자바에서 모든 상속은 public 상속이다; private과 protected 상속의 C++특징과 유사성이 없다.
```

*extends* 키워드는 당신이 기본 클래스에서 파생된 새로운 클래스를 생성한다는 것을 나타낸다.
기본 클래스는 superclass, base class, parent class 라고 불린다.
새로운 클래스는 subclass, derived class, child class 라고 불린다.
슈퍼클래스와 서브클래스 용어는 자바 프로그래머에 의해 가장 흔히 사용된다, 비록 몇몇 프로그래머들이 부모/자식 비유를 선호하지만, 이것은 또한 "상속" 주제와 함께 병행한다.

*Employee* 클래스는 슈퍼클래스이나, 그것이 서브클래스보다 우월하거나 더 많은 기능을 포함하고 있기 때문은 아니다.
사실, 그 반대는 사실이다 : 서브클래스는 슈퍼클래스보다 더 많은 기능을 가지고 있다.
예를 들면, 우리가 *Manager* 클래스 코드의 나머지 부분을 살펴보면 알 수 있듯이, *Manager* 클래스는 슈퍼클래스 *Employee* 보다 더 많은 정보를 요약화하고, 더 많은 기능을 가진다.

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

물론, 만약 당신이 Employee 객체를 가지고 있다면, 당신은 setBonus 메소드를 적용할 수 없다 - Employee 클래스에서 정의된 메소드가 아니다.

그러나 당신은 Manager객체의 getName, getHireDay 와 같은 메소드를 사용할 수 있다.
비록 이 메소드들이 Manager클래스에서 명확하게 정의되지 않았더라도, Employee 슈퍼클래스로부터 자동적으로 상속받을 수 있다.

비슷하게, name, salary, hireDay 필드들은 슈퍼클래스로부터 가져온다.
모든 Manager 객체가 name, salary, hrieDay, bonus 필드를 가지고 있다.

슈퍼클래스를 상속받은 서브클래스를 정의할 때, 당신은 오직 서브클래스와 슈퍼클래스 사이의 차이점을 나타내는 것을 필요로 한다.
클래스를 설계할 때, 당신은 슈퍼클래스에서 가장 일반적인 메소드를 사용하고, 서브클래스에서 더 전문적인 메소드를 사용한다.
슈퍼 클래스로 옮겨서 공통의 기능을 알아내는 것은 객체 지향 프로그래밍에서 흔히 볼 수 있다.

#### **5-1-2 메소드 오버라이딩**

슈퍼클래스 메소드들 중 일부는 Manager 서브클래스에 적합하지 않다.
특히, getSalary 메소드는 base salary와 bonus의 합계를 반환하여야한다.
당신은 슈퍼클래스 메소드를 재정의(Override)한 새로운 메소드를 제공하는것이 필요하다.

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
언뜻 보기에는 간단한 것처럼 보인다 - 단지 salary와 bonus 필드의 합계를 반환해라.

```
public double getSalary()
{
    return salary + bonus;  // won't work
}
```

그러나, 작동하지 않을 것이다.
오직 Employee메소드가 Employee클래스의 private필드에 직접 접근할 수 있다는 것을 상기해라.
이것은 Manager클래스의 getSalary메소드가 salary필드에 직접 접근할 수 없다는 것을 의미한다.
만약 Manager메소드가 그들의 private필드에 접근하는 것을 원한다면, 그들은 모든 다른 메소드가 하는 것을 해야한다 - public 인터페이스를 사용해라, 이 경우에 Employee클래스의 public getSalary메소드를 사용한다.

다시 시도해보자. 당신은 salary 필드에 간단하게 접근하는 것 대신에 getSalary를 호출하는 것을 필요로 한다 :

```
public double getSalary()
{
    double baseSalary = getSalary();    // still won't work
    return baseSalary + bonus;
}
```

문제는 getSalary를 호출하는 것이 간단하게 스스로를 호출한다는 것이다, 왜냐하면 Manager클래스가 getSalary메소드(다시 말해, 그 우리가 구현하고자 하는 메소드)를 가지고 있기 때문이다.
그 결과는 같은 메소드를 호출하는 것의 무한한 연속이고, 프로그램 충돌로 이어진다.

우리는 우리가 현재 클래스가 아닌, Employee슈퍼클래스의 getSalary메소드 호출을 원하는 것을 나타내는 것을 필요로 한다.
당신은 이 목적을 위해 특별한 키워드 super을 사용한다.

`super.getSalary()`은 Employee클래스의 getSalary메소드를 호출한다.
Manager클래스의 getSalary메소드의 옳은 버전이 있다. :

```
public double getSalary()
{
    double baseSalary = super.getSalary();
    return baseSalary + bonus;
}
```

```
필기 : 몇몇 사람들은 super을 this참조와 비슷하다고 생각한다.
그러나 그 유추는 꽤 정확하지 않다 : super은 객체의 참조가 아니다.
예를 들면, 당신은 또 다른 object변수에 super값을 할당할 수 없다.
대신에, super는 컴파일러에게 슈퍼클래스 메소드를 호출하라고 지시하는 특별한 키워드이다.
```

당신도 봤듯이, 서브클래스는 필드를 추가할 수 있고, 메소드를 추가하거나, 슈퍼클래스의 메소드를 재정의 할 수 있다.
그러나, 상속은 결코 어느 필드나 메소드를 가져갈 수 없다.

```
C++ 필기 : 자바는 슈퍼클래스 메소드를 호출하는 super키워드를 사용한다.
C++에서는, 대신에 당신은 :: 연산자와 함께 슈퍼클래스의 이름을 사용할 것이다.
예를 들면, Manager클래스의 getSalary메소드는 super.getSalary 대신에 Employee::getSalary를 호출할 것이다.
```

#### **5-1-3 서브클래스 생성자**

이 예시를 완료하기 위해, 생성자를 제공하자.

```
public Manager(String name, double salary, int year, int month, int day)
{
    super(name, salary, year, month, day);
    bonus = 0;
}
```

여기, super키워드는 다른 의미를 가지고 있다.
이 명령
`super(n, s, year, month, day);`
는 "Employee슈퍼클래스의 생성자를 매개변수 n, s, year, month, day와 함께 호출해라" 의 약칭이다.
Manager생성자가 Employee클래스의 private필드에 접근할 수 없을 때부터, 생성자를 통해 그들을 초기화 해야한다.
생성자는 특별한 super문법에서 호출된다.
super을 사용하는 호출은 서브클래스의 생성자에서 첫 문장이 되어야한다.

만약 서브클래스 생성자가 슈퍼클래스 생성자를 명확하게 호출하지 않는다면, 슈퍼클래스의 인수가 없는 생성자가 호출된다.
만약 슈퍼클래스가 인수가 없는 생성자를 가지고 있지 않고 서브클래스 생성자가 또 다른 슈퍼클래스 생성자를 명확하게 호출하지 않는다면, 자바 컴파일러는 에러를 제출한다.

```
필기 : this 키워드가 두 가지 의미를 가지고 있다는 것을 상기해라 : 암묵적 매개변수에 대한 참조를 나타내는 것과 같은 클래스의 또 다른 생성자를 호출하는 것.
마찬가지로, super키워드는 두가지 의미를 가진다 : 슈퍼클래스 메소드를 호출하는 것과 슈퍼클래스 생성자를 호출하는 것.
생성자를 호출하곤 했을 때, this와 super키워드는 면밀하게 관련이 있다.
생성자 호출은 오직 또 다른 생성자에서 첫 문장으로서 발생할 수 있다.
생성자 매개변수는 같은 클래스(this)의 또 다른 생성자나 슈퍼클래스(super)의 생성자를 넘겨받는다. 
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

당신이 Manager객체에 getSalary메소드를 재정의한 후, managers는 그들의 salaries가 더해진 bonus를 자동적으로 가지게 될 것이다.
작업에서 이런 예시가 있다.
우리는 새로운 manager를 만들고, manager의 bonus를 설정한다.

```
Manager boss = new Manager("Carl Cracker", 80000, 1987, 12, 15);
boss.setBonus(5000);
```

우리는 세 개의 employee의 배열을 만든다. 

`Employee[] staff = new Employee[3];`

우리는 managers와 employees의 혼합물과 함께 배열에 이주시킨다.

```
staff[0] = boss;
staff[1] = new Employee("Harry Hacker", 50000, 1989, 10, 1);
staff[2] = new Employee("Tony Tester", 40000, 1990, 3, 15);
```

우리는 모두의 salary를 출력한다.

```
for(Employee e : staff)
    System.out.println(e.getName() + " " + e.getSalary());
```

이 루프는 다음의 정보를 출력한다.

```
Carl Cracker 85000.0
Harry Hacker 50000.0
Tommy Tester 40000.0
```

이제 staff[1]과 staff[2]는 그들이 Employee객체이기 때문에 각각 그들의 base salary를 출력한다.
그러나, staff[0]은 Manager객체이다. Manager객체의 getSalary메소드는 bonus를 base salary에 더한다.
주목할만한 것은 `e.getSalary()` 호출이 옳은 getSalary메소드를 알아낸다.
e의 선언된 타입은 Employee 임에 주목해라.
그러나, e가 참조한 객체의 실제 타입은 Employee 또는 Manager가 될 수 있다.

e가 Employee객체를 참조할 때, e.getSalary()는 Employee클래스의 getSalary메소드를 호출한다.
**그러나, e가 Manager객체를 참조할 때, Manager클래스의 getSalary메소드가 호출된다.**
가상머신은 e가 나타내는 객체의 실제 타입에 대해서 알기 때문에 옳은 메소드를 호출할 수 있다.

(변수 e와 같은)객체 변수가 다중의 실제 타입을 참조할 수 있다는 사실은 **다형성**이라 불린다.
실행 시에 자동으로 적절한 메소드를 선택하는 것은 **동적결합(동적바인딩(dynamic binding))**이라고 불린다.
우리는 이 장에서 두 주제를 좀 더 자세하게 논의한다.

```
C++ 필기 : C++에서, 만약 당신이 동적 바인딩을 원한다면, 당신은 가상으로서 member function을 선언하는 것을 필요로 한다.
자바에서, 동적 바인딩은 디폴트 행동이다; 만약 당신이 가상으로된 메소드를 원하지 않는다면, 당신은 final로서 그것을 태그한다.
(우리는 이 장에서 나중에 final키워드에 대하여 논의한다.)
```

Listing 5.1은 어떻게 salary계산이 Employee(Listing 5.2)와 Manager(Listing 5.3)객체와 차이가 있는지 보여주는 프로그램을 포함한다.

```
Listing 5.1     inheritance/ManagerTest.java

package inheritance;

/**
    * This program demonstrates inheritance.
    * @version 1.21 2004-02-21
    * @author Cay Horstmann
    */
public class ManagerTest
{
    public static void main(String[] args)
    {
        // construct a Manager object
        Manager boss = new Manager("Carl Cracker", 80000, 1987, 12, 15);
        boss.setBonus(5000);

        Employee[] staff = new Employee[3];

        // fill the staff array with Manager and Employee objects
        staff[0] = boss;
        staff[1] = new Employee("Harry Hacker", 50000, 1989, 10, 1);
        staff[2] = new Employee("Tommy Tester", 40000, 1990, 3, 15);

        // print out information about all Employee objects
        for(Employee e : staff)
            System.out.println("name=" + e.getName() + ",salary=" + e.getSalary());
    }
}
```

```
Listing 5.2     inheritance/Employee.java

package inheritance;

import java.time.*;

public class Employee
{
    private String name;
    private double salary;
    private LocalDate hireDay;

    public Employee(String name, double salary, int year, int month, int day)
    {
        this.name = name;
        this.salary = salary;
        hireDay = LocalDate.of(year, month, day);
    }

    public String getName()
    {
        return name;
    }

    public double getSalary()
    {
        return salary;
    }

    public LocalDate getHireDay()
    {
        return hireDay;
    }

    public void raiseSalary(double byPercent)
    {
        double raise = salary * byPercent / 100;
        salary += raise;
    }
}
```

```
Listing 5.3     inheritance/Manager.java

package inheritance;

public class Manager extends Employee
{
    private double bonus;

    /**
        * @param name the employee's name
        * @param salary the salary
        * @param year the hire year
        * @param month the hire month
        * @param day the hire day
        */
    public Manager(String name, double salary, int year, int month, int day)
    {
        super(name, salary, year, month, day);
        bonus = 0;
    }

    public double getSalary()
    {
        double baseSalary = super.getSalary();
        return baseSalary + bonus;
    }

    public void setBonus(double b)
    {
        bonus = b;
    }
}
```

#### **5-1-4 상속 계층**

상속은 클래스의 한층을 가져오는 것을 멈출 필요가 없다.
예를 들면, 우리는 Manager을 상속받은 Excutive클래스를 가질 수 있었다.
공통 슈퍼클래스를 상속받은 모든 클래스의 컬렉션은 상속 계층?(inheritance hierarchy)라고 불리고, Figure 5.1에서 보여진다.
상속 계층에서 특정한 클래스로부터 조상에 이르는 길은 이것의 상속 체인(inheritance chain)이다.

```
Figure 5.1  Employee inheritance hierarchy

            Employee
        ___________↑______________       
    |           |              |
Manager     Secretary      Programmer
    ↑
Executive
```

보통 먼 조상클래스로부터 불려받은 한 체인보다 많이 있다. //
당신은 Employee를 상속받은 서브클래스 Programmer 또는 Secretary를 형성할 수 있었고, 그들은 Manager클래스와는 관계가 없다.
이 과정은 필요한 한 계속될 수 있다.

```
C++ 필기 : C++에서, 한 클래스는 다중의 슈퍼클래스를 가질 수 있다.
자바는 다중 상속을 지원할 수 없다.
다중 상속의 기능의 대부분을 회복하는 방법을 위해, 288쪽에 Section 6.1, "인터페이스"를 보자.
```

---
#### **5-1-5 다형성**
---

간단한 규칙은 당신이 상속이 당신의 데이터에 옳은 설계인지 아닌지 결정하는 것을 도울 수 있다.
"is-a" 규칙은 서브클래스의 모든 객체가 슈퍼클래스의 객체라는 것을 말한다.
예를 들면, 모든 manager은 employee이다.
그러므로, 그것은 Employee클래스의 서브클래스가 되는 Manager클래스가 된다.
물론, 그 반대는 사실이 아니다 - 모든 employee가 manager는 아니다.

"is-a" 규칙을 표현하는 또 다른 방법은 substitution principle 이다.
그 원칙은 당신은 프로그램이 슈퍼클래스 객체를 상속할 때마다 서브클래스 객체를 사용할 수 있다는 것을 말한다.

예를 들면, 당신은 서브클래스 객체를 슈퍼클래스 변수에 할당할 수 있다.

```
Employee e;
e = new Employee(...);  // Employee object expected
e = new Manager(...);   // OK, Manager can be used as well
```

자바 프로그래밍 언어에서 객체 변수는 다형성이다.
Employee타입의 변수는 Employee타입의 객체 또는 Employee클래스의 어떤 서브클래스의 객체를 참조할 수 있다(Manager, Executive, Secretary).

우리는 Listing 5.1에서 이 원칙을 이용한다.

```
Manager boss = new Manager(...);
Employee[] staff = new Employee[3];
staff[0] = boss;
```

이 경우에는, staff[0]와 boss의 변수는 같은 객체를 나타낸다.
그러나, staff[0]은 컴파일러에 의해 오직 Employee객체로 여겨진다.

그것은 당신이 `boss.setBonus(5000); // OK` 호출할 수 있다는 것을 의미한다.
그러나 당신은 `staff[0].setBonus(5000); // Error` 호출할 수 없다.

staff[0]의 선언 타입은 Employee이고, setBonus메소드는 Employee클래스의 메소드가 아니다.

그러나, 당신은 서브클래스 변수에 슈퍼클래스 참조를 할당할 수 없다.
예를 들면, 이 할당을 만드는 것은 합법이 아니다.

`Manager m = staff[i];  // Error`

그 이유는 명백하다: 모든 employee가 manager은 아니다.
만약 이 할당이 성공하려면, 그리고 m이 manager이 아닌 Employee객체에 참조되려면, m.setBonus(...) 호출이 가능하게 될것이고, runtime error가 발생할 것이다.    //

```
be to 용법
예정 ~할 예정이다
의무 ~해야한다
가능 ~할 수 있다
운명 ~할 운명이다
의도 ~하려면, ~되려면
```

```
!주의 : 자바에서, 서브클래스 참조 배열은 cast없이 슈퍼클래스 참조 배열을 변환될 수 있다.
예를 들면, manager의 이 배열을 고려해라.

    Manager[] managers = new Manager[10];

이 배열을 Employee[]배열로 변환하는 것은 합법이다.

    Employee[] staff = managers;    // OK

물론, 당신은 생각할지도 모른다.
결국에는, 만약 managers[i]가 Manager이라면, 또한 Employee이다.
그러나 실제로, 놀라운 어떤 것은 진행 중이다.
managers와 staff가 같은 배열 참조라는 점을 명심해라

    staff[0] = new Employee("Harry Hacker", ...);

컴파일러는 기꺼이 이 할당을 허락할 것이다.
그러나 staff[0]와 managers[0]은 같은 참조여서, 마치 우리가 단지 employee가 management ranks를 밀수하는것을 managed 한 것 처럼 보인다.
저것은 매우 나쁘다 - managers[0].setBonus(1000)을 호출하는 것은 존재하지 않는 instance field에 접근하는 것을 시도할 것이고, 이웃 메모리를 손상시킬 것이다.
이러한 손상을 발생하지 않도록, 모든 배열은 그들이 생성했던 그 요소 타입을 기억하고, 그들은 오직 호환 가능한 참조가 그들에 저장된다는 것을 감시한다.
예를 들면, new Manager[10]으로 생성된 그 배열은 그것이 managers의 배열이라는 것을 기억한다.
Employee참조를 저장하는 것을 시도하는 것은 ArrayStoreException을 야기한다.
```

---
#### **5-1-6 메소드 호출 이해**
---

어떻게 메소드 호출이 객체에 적용되는지 확실하게 이해하는 것은 중요하다.
우리가 x.f(args)를 호출한다고 말하고, 그 포함되는 매개변수 x는 C클래스의 객체로 선언된다.
결과는 이렇다:
    1. 컴파일러는 객체와 메소드 이름의 선언된 타입을 본다.
    같은 이름을 가지고 있지만 다른 매개변수 타입을 가진 다수의 메소드, f, 가 있을지도 모른다는 점을 참고해라.
    예를 들면, 메소드 f(int)와 f(String)이 있을 수 있다.
    컴파일러는 C클래스에서 f라 불리는 모든 메소드와 C의 슈퍼클래스에서 f라 불리는 모든 접근 가능한 메소드를 열거한다. (슈퍼클래스의 Private메소드는 접근 불가능하다.)
    이제 컴파일러는 호출되는 메소드의 모든 가능한 후보자들을 안다.
    
    2. 다음, 컴파일러는 메소드 호출에서 공급되는 인수의 타입을 결정한다.
    만약 f로 호출되는 모든 메소드들 사이에 공급되는 인수에 매개 변수 타입이 가장 매치되는 독특한 메소드가 있다면, 그 메소드는 호출되는 것으로 선정된다.
    이 과정은 overloading resolution 이라고 불린다.
    예를 들면, x.f("Hello") 호출에서, 컴파일러는 f(String)과 f(int)가 아닌 것을 pick 한다.
    이 상황은 타입 변환(int 에서 double, Manager 에서 Employee, 기타 등등)때문에 컴플렉스를 가질 수 있다.
    만약 그 컴파일러가 매개변수와 매치되는 어떤 메소드를 찾을 수 없다면, 또는, 다중의 메소드들이 변환이 적응된 후에도 모두 매치된다면, 그 컴파일러는 오류를 제출한다.
    
    이제 그 컴파일러는 호출되는 것을 필요로 하는 메소드의 이름과 매개변수 타입을 안다.

    ```
    필기 : 메소드의 이름과 매개변수 타입 목록은 메소드의 시그니처로 호출된다는 것을 회상해라.
    예를 들면, f(int)와 f(String)은 같은 이름이나 다른 시그니처를 가진 두 메소드이다.
    만약 당신이 슈퍼클래스 메소드로서 같은 시그니처를 가지고 있는 서브클래스에서 메소드를 정의한다면, 당신은 슈퍼클래스 메소드를 오버라이드한다.

    그 반환 타입은 시그니처의 부분이 아니다.
    그러나, 당신이 메소드를 오버라이드 할 때, 당신은 호환 가능한 반환 타입을 유지하는 것을 필요로 한다.
    서브클래스는 반환 타입을 오리지널 타입의 서브타입으로 바꿀지도 모른다.
    예를 들면, Employee클래스가
        public Employee getBuddy() { ... }
        메소드를 가지고 있다고 가정해라.
    manager은 buddy로서 낮은 employee를 가지는 것을 결코 원하지 않을 것이다.
    Manager 서브클래스는 
        public Manager getBuddy() { ... } // OK to change return type
        이 메소드를 오버라이드 할 수 있다는 사실을 반영하면,
        우리는 두 getBuddy 메소드들이 공변하는 반환 타입을 가지고 있다고 말한다.
    ```

    3. 만약 메소드가 private, static, final, 또는 생성자라면, 컴파일러는 정확하게 어떤 메소드를 호출할 지 안다.
    그 final 수식어는 다음 섹션에서 설명된다.
    이것은 정적 바인딩(static binding)이라 불린다.
    그렇지 않으면, 그 호출되는 메소드가 암시의 매개변수의 실제 타입에 의존하고, 동적 바인딩은 실행 중에 사용되어야 한다.
    예를 들면, 그 컴파일러는 동적바인딩과 함께 f(String)를 호출하는 명령어를 생성할 것이다.

    4. 프로그램이 실행하고 메소드를 호출하는 동적바인딩을 사용할 때, 그 가상머신은 x를 참조한 오브젝트의 실제 타입에 적합한 메소드의 버전을 호출하여야 한다.
    실제 타입이 C의 서브클래스, D라고 말하자.
    만약 D클래스가 f(String)메소드를 정의한다면, 그 메소드는 호출된다.
    만약 아니라면, D의 슈퍼클래스는 f(String)메소드와 기타 등을 검색한다.

    메소드가 호출될 때마다 이 탐색을 이행하는 데 시간이 많이 걸린다.
    그러므로, 가상머신은 모든 메소드 시그니처들과 호출되는 실제 메소드들을 나열한 각 클래스 메소드 테이블을 미리 계산한다.
    메소드가 실제로 호출될 때, 그 가상머신은 간단하게 표를 탐색한다.
    예를 들면, 그 가상머신은 D클래스의 메소드 테이블을 찾아보고, f(String)을 호출하는 메소드를 탐색한다.
    그 메소드는 X가 D의 슈퍼클래스의 일부인 곳에서, D.f(String) 또는 X.f(String)이 될지도 모른다.
    이 시나리오를 전환하는 한가지가 있다.
    만약 그 호출이 super.f(param)이라면, 컴파일러는 그 암시의 매개변수의 슈퍼클래스의 메소드 테이블을 찾아본다.

Listing 5.1에서 e.getSalary()호출에서 이 과정을 자세하게 보자.
e의 선언된 타입은 Employee이다.
Employee클래스는 메소드 매개변수가 없는 getSalary라 불리는 하나의 메소드를 가지고 있다.
그러므로, 이 경우에 있어서, 우리는 오버로딩 해결에 대해서 걱정하지 않는다.

그 getSalary메소드는 private, static, final이 아니라서, 동적으로 바운드한다.
그 가상머신은 Employee와 Manager클래스의 메소드 테이블을 소개한다.
Employee 테이블은 Employee클래스에서 정의된 것이라고 보여준다:
    
    Employee:
        getName() -> Employee.getName()
        getSalary() -> Employee.getSalary()
        getHireDay() -> Employee.getHireDay()
        raiseSalary(double) -> Employee.raiseSalary(double)

실제로, 그것은 전체의 이야기가 아니다 - 당신이 나중에 이 장을 본다면, 그 Employee클래스는 많은 메소드를 상속하는 Object슈퍼클래스 가지고 있다.
우리는 이제 Object메소드를 무시한다.

그 Manager메소드 테이블은 미세하게 다르다.
세 개의 메소드는 상속 받고, 한 메소느는 재정의 되고, 한 메소드는 추가된다.

    Manager:
        getName() -> Employee.getName()
        getSalary() -> Manager.getSalary()
        getHireDay() -> Employee.getHireDay()
        raiseSalary(double) -> Employee.raiseSalary(double)
        setBonus(double) -> Manager.setBonus(double)

실행 중에, e.getSalary() 호출은 다음과 같이 해결된다:
    1. 처음에, 그 가상머신은 e의 실제 타입의 메소드 테이블을 가져온다.
    저것은 Employee, Manager, 또는 또 다른 Employee의 서브클래스의 테이블이 될지도 모른다.
    2. 그러면, 그 가상머신은 getSalary()시그니처를 정의한 클래스를 탐색한다.
    이제 어떤 메소드를 호출할 지 안다.
    3. 마지막, 가상머신은 그 메소드를 호출한다.

동적바인딩은 매우 중요한 속성을 가진다:
기존 코드를 수정할 필요 없이 프로그램을 확장 가능하게 한다.
새로운 클래스 Executive가 추가되고 변수 e가 그 클래스의 객체를 참조한다는 가능성이 있다고 가정해라.
e.getSalary()호출을 포함하는 코드는 재컴파일될 필요가 없다.
Executive.getSalary()메소드는 만약 e가 Executive타입의 객체를 참조한다면 자동으로 호출된다.

```
!주의 : 당신이 메소드를 오버라이드할 때, 그 서브클래스 메소드는 적어도 슈퍼메소드만큼 보여야 한다.
특히, 만약 그 슈퍼클래스 메소드가 public 이라면, 서브클래스 메소드는 오직 public 으로 선언되어야 한다.
서브클래스 메소드의 public 지정자를 우연히 생략하는 것은 흔한 오류이다.
그러면 그 컴파일러는 당신이 더 제한적인 접근 권한을 제공하려고 하는 것을 불평한다.
```

---
#### **5-1-7 상속 방지?(Preventing Inheritance) : Final클래스와 메소드**
---

때떄로, 당신은 누군가가 당신의 클래스의 하나로부터 서브클래스를 형성하는 것을 방지하기를 원한다.
상속할 수 없는 클래스는 final클래스라고 불리고, 당신은 이것을 나타내는 클래스의 정의에서 final 수식어를 사용한다.
예를 들면, 우리가 다른 사람이 Executive클래스를 서브클래스화하는 것을 방지하기를 원한다고 가정해라.
간단히 final 수식어를 사용한 클래스를 선언해라, 다음과 같이:

    ```
    public final class Executive extends Manager
    {
        ...
    }
    ```

당신은 또한 final클래스 안에서 특정 메소드를 생성할 수 있다.
만약 당신이 이것을 한다면, 서브클래스는 그 메소드를 재정의(오버라이드) 할 수 없다.(final클래스에서 모든 메소드는 자동으로 final이다.)
예를 들면:
    
    ```
    public class Employee
    {
        ...
        public final String getName()
        {
            return name;
        }
        ...
    }
    ```

```
필기 : 필드는 오직 final로 선언될 수 있다는 것을 리콜해라.
final필드는 그 객체가 생성된 후에 변경될 수 없다.
그러나, 만약 클래스가 final로 선언된다면, 필드가 아닌, 오직 그 메소드들은 자동으로 final이다.
```

오직 final메소드 또는 클래스를 만드는 한가지 좋은 이유가 있다:
서브클래스에서 그것의 의미가 변경될 수 없도록 하기 위해서이다.
예를 들면, Calendar클래스의 getTime과 setTime메소드는 final이다.
이것은 Calendar클래스의 설계자가 Date클래스와 calendar state 사이의 변환을 위한 책임감을 떠맡았다는 것을 나타낸다.
서브클래스는 이 방식을 엉망으로 만드는 것이 허락되지 말아야한다.
비슷하게, String클래스는 final클래스이다.
저것은 아무도 String의 서브클래스를 정의할 수 없다는 것을 의미한다.
다시 말해서, 만약 당신이 String참조를 가지고 있다면, 당신은 그것이 String 그리고 오직 String을 참조한다는 것을 안다.

몇몇 프로그래머들은 당신이 다형성을 원하는 좋은 이유를 가지고 있지 않다면 final로서 모든 메소드들을 선언해야한다고 믿는다.
사실, C++과 C#에서, 당신이 분명히 요청하지 않는다면, 메소드들은 다형성을 사용하지 않는다.
저것은 조금 극단적인 것일지도 모른다. 그러나, 당신이 클래스 계급을 설계할 때, 우리는 final메소드와 클래스에 대해 신중히 생각하는 것은 좋은 생각이라는 것에 동의한다.

자바 초기에, 몇몇 프로그래머들은 동적바인딩의 overhead를 피하기 위해 final키워드를 사용했다.
만약 메소드가 재정의되지 않고, short라면, 컴파일러는 그 메소드 호출을 최적화 할 수 있다 - 과정은 inlining 이라 불린다.
예를 들면, e.getName()호출을 인라이닝하는 것은 e.name에 접근하는 필드로 대체한다.
이것은 개선할만한 가치가 있다-현재 명령을 실행하는 동안 CPU는 그들의 instruction을 prefetching하는 전략을 방해하기 때문에 분기를 싫어한다.
그러나, 만약 getName이 또 다른 클래스에서 재정의 될 수 있다면, 컴파일러는 재정의 코드가 할지도 모르는 것을 아는 방법이 없기 때문에 인라인할 수 없다.

운좋게도, 가상머신에서 적시 컴파일러는 전통적인 컴파일러보다 더 나은 작업을 수행할 수 있다.
어떤 클래스가 주어진 클래스를 상속하는지 확실하게 알고, 어떤 클래스가 주어진 메소드를 실제로 재정의할 수 있는지 확인할 수 있다.
만약 메소드가 짧다면, 빈번하게 호출된다면, 그리고 실제로 재정의 되지 않는다면, 적시 컴파일러는 그 메소드를 인라인할 수 있다.
만약 가상머신이 인라인된 메소드를 재정의하는 또 다른 서브클래스를 불러온다면 무슨 일이 일어날까?
그러면 그 최적화는 그 인라이닝을 무효로 만들것이다.
시간이 걸리지만, 거의 일어나지 않는다.
    
---
#### **5-1-8 캐스팅**
---

3장에서 한 타입에서 또 다른 타입으로의 변환을 강화하는 과정을 캐스팅이라 불리는 것을 상기해라.
자바 프로그래밍 언어는 캐스트를 위한 특별한 표기법을 가지고 있다.
예를 들면,

    ```
    double x = 3.405;
    int nx = (int) x;
    ```
x표현의 값을 integer로 변환하고, 분수 부분을 버린다.

때때로 부동 소수점 숫자를 정수로 변환하는 것을 필요로 하는 것처럼, 당신은 객체 참조를 한 클래스에서 다른 클래스로 변환하는 것을 필요로 할지도 모른다.
실제로 객체 참조의 캐스트를 만드는 것은, 숫자 식을 캐스팅하기 위해 사용하는 것과 비슷한 문법을 사용해라.
대상 클래스 이름을 괄호로 둘러싸고, 당신이 캐스트를 원하는 객체 참조 앞에 배치시켜라.
예를 들면 :

`Manager boss = (Manager) staff[0];`

당신이 캐스트를 만들기를 원하는 한가지 이유가 있다 - 그것의 실제 타입이 일시적으로 잊어버린 후에 최대 가용성으로 객체를 사용하는 것
예를 들면, ManagerTest클래스에서, 그것의 몇몇 요소들이 보통 employees였기 때문에 staff배열은 Employee객체의 배열이 되어야 했다.
우리는 새로운 변수에 접근하기 위해 배열의 관리요소들을 Manager에게 다시 캐스트를 필요로 할 것이다.
(첫 번째 섹션의 샘플 코드에서, 우리는 캐스트를 피하기 위해 특별한 노력을 기울였다는 점에 유의한다.
배열에서 그것을 저장하기 전에 우리는 boss변수를 Manager객체로 초기화했다.)

당신도 알다시피, 자바에서 모든 변수는 타입을 가지고 있다.
타입은 변수가 참조하고 그것이 할 수 있는 객체의 종류를 묘사한다.
예를 들면, staff[i]는 Employee객체를 참조한다(그래서 이것은 또한 Manager객체를 참조한다).

컴파일러는 당신이 변수에 값을 저장할 때 너무 많이 약속하지 않는다는 것을 체크한다.
만약 당신이 서브클래스 참조를 슈퍼클래스 변수에 할당한다면, 당신은 덜 유망할 것이고, 그리고 컴파일러는 당신이 그것을 하라고 간단히 시킬 것이다.
만약 당신이 슈퍼클래스 참조를 서브클래스 변수에 할당한다면, 당신은 더 유망할 것이다.
그러면 당신은 실행 중에 당신의 약속이 체크될 수 있도록 캐스트를 사용해야 한다.

만약 당신이 상속체인을 cast down하고, 객체가 포함하는 것에 대해 "거짓말" 한다면 어떻게 될까?

    Manager boss = (Manager) staff[1]; // Error

프로그램이 실행할 때, 자바 런타임 시스템은 깨진 약속을 알리고, ClassCastException을 발생한다.
만약 당신이 예외를 잡지 않는다면, 당신의 프로그램은 종료된다.
그러므로 이것은 시도하기 전에 캐스트가 성공할 것인지 아닌지 찾아내는 좋은 프로그래밍 연습이다.
간단히 instanceof 연산자를 사용해라.
예를 들면:

```
if (staff[1] instanceof Manager)
{
    boss = (Manager) staff[1];
    ...
}
```

마침내, 컴파일러는 만약 성공적인 캐스트의 기회가 없다면당신이 캐스트 하는 것을 시키지 않을 것이다.
예를 들면, 캐스트

```
String c = (String) staff[1];
```

은 compile-time 오류이다. 왜냐하면 String은 Employee의 서브클래스가 아니기 때문이다.

요약해서 말하면:
    - 당신은 상속 계층 내에 캐스트 할 수 있다
    - 서브클래스에서 슈퍼클래스로부터 캐스팅 전에 확인하기 위해 instanceof를 사용해라.

```
필기 : 그 테스트
x instanceof C
는 만약 x가 null이라는 예외를 발생하지 않는다.
단순히 false를 반환한다.
그것은 이해하기 쉽다:
null은 어떤 객체를 참조하지 않아서, 분명히 타입C의 객체를 참조하지 않는다.
```

실제로, 캐스트에 의해 객체의 타입을 변환하는 것은 일반적으로 좋은 생각이 아니다.
이 예제에서 당신은 대부분의 목적을 위해 Manager객체에서 Employee객체를 캐스트할 필요가 없다.
getSalary메소드는 두 개의 클래스의 두 객체에서 올바르게 작동할 것이다.
다형성을 만드는 동적바인딩은 자동으로 올바른 메소드를 위치시킨다.
캐스트를 만드는 이유는 setBonus와 같은 managers에서 독특한 메소드를 사용하는 것이다.
만약 어떤 이유로 당신이 Employee객체에서 setBonus를 호출하는 것을 원한다면, 이것이 슈퍼클래스에서 설계 결함을 나타내는 것인지 자문해라.
슈퍼클래스와 재설계하고 setBonus메소드를 추가하는 것이 이해하기 쉬울지도 모른다.
당신의 프로그램을 종료하려면 ClassCastException 이 하나만 필요하다는 것을 기억해라.
보통, 캐스트와 instanceof연산자의 사용을 최소화하는것이 최선이다.

```
C++ 필기:
자바에서 C의 "bad old days"로 부터 캐스트 문법을 사용하지만, C++의 dynamic_cast연산자와 같이 작동한다.
예를 들면,
    Manager boss = (Manager) staff[1]; // Java
는 한가지 중요한 차이를 가지고
    Manager* boss = dynamic_cast<Manager*>(staff[1]); // C++
와 같다.
만약 캐스트가 실패한다면, null객체를 넘겨주는게 아니라 예외를 던진다.
이런 의미에서, C++  references의 캐스트와 같다.
이것을 골칫거리이다.
C++에서, 당신은 한 연산자에서 타입 테스트와 타입 변환을 처리할 수 있다.
    Manager* boss = dynamic_cast<Manager*>(staff[1]); // C++
    if(boss != NULL) ...
자바에서, 당신은 instanceof연산자와 캐스트의 결합을 사용하는 것을 필요로한다.
    if(staff[1] instanceof Manager)
    {
        Manager boss = (Manager)staff[1];
        ...
    }

```

---
#### **5-1-9 추상 클래스**
---

당신이 상속 계층이 상승함으로써, 클래스는 더 일반적이고 아마 더 추상적이게 된다.
적절한 시점에, 그 조상 클래스가 너무 일반적으로 되어 당신은 사용하기를 원하는 인스턴스를 가진 클래스보다 다른 클래스를 위한 기준으로 더 많이 생각하게 된다.
예를 들면, Employee클래스 계층의 상속을 고려해라.
employee는 person이면서 student이다.
Person과 Student를 포함하는 클래스 계층을 상속해라.
Figure 5.2 는 이 클래스 사이의 상속 관계를 보여준다.

왜 추상적인 개념의 단계가 둘 다 매우 높냐?
이름과 같이 모든 사람들이 이해하기 쉬운 몇가지 속성이 있다.
student와 employee 둘다 이름을 가지고 있고, 흔한 슈퍼클래스는 getName메소드를 제외하라고 한다. 상속 계층에서 높은 단계로

이제 또 다른 메소드 getDescription을 추가해보자. 이 메소드의 목적은
    an employee with a salary of $50,000.00
    a student majoring in computer science
와 같은 사람의 짧은 묘사를 반환하는 것이다.

```
- Figure 5.2

        Person
    ____↑____
    |         |
Employee  Student
```

Employee와 Student클래스의 메소드를 구현하는 것은 쉽다.
그러나 Person클래스에서 어떤 정보를 제공할 수 있을까?
Person클래스는 person에 대해 이름 이외에 어떤 것도 알지 못한다.
물론, 당신은 빈 문자열을 반환하는 Person.getDescription()을 구현할 수 있었다.
그러나 더 나은 방법이 있다.
만약 당신이 abstract 키워드를 사용한다면, 당신은 메소드를 전혀 구현할 필요가 없다.

    public abstract String getDescription();
        // no implementation required

추가적인 명확성을 위해, 하나 이상의 추상 메소드를 가지는 클래스 자체가 추상적이라고 선언되어야 한다.

    public abstract class Person
    {
        ...
        public abstract String getDescription();
    }

추상메소드에 더하여, 추상 클래스는 필드와 구체적인 메소드를 가질 수 있다.
예를 들면, Person클래스는 사람의 이름을 저장하고 이것을 반환하는 구체적인 메소드를 가진다.

    public abstract class Person
    {
        private String name;

        public Person(String name)
        {
            this.name = name;
        }

        public abstract String getDescription();

        public String getName()
        {
            return name;
        }
    }

```
팁 : 몇몇 프로그래머들은 추상클래스가 구체적인 메소드를 가질 수 있다고 깨닫지 못한다.
당신은 항상 흔한 필드와 메소드(추상이거나 아니거나)를 슈퍼클래스(추상이거나 아니거나)로 움직여야 한다.
```

추상메소드는 서브클래스에서 구현된 메소드를 위해 플레이스 홀더로서 역할을 한다.
당신이 추상클래스를 상속할 때, 당신은 두 가지 선택권을 가지고 있다.
당신은 몇몇 또는 모든 정의되지 않은 추상메소드를 남길 수 있다; 그러면 당신은 서브클래스를 더 추상적으로? 태그해야 한다.
또는 당신은 모든 메소드를 정의할 수 있고, 서브클래스는 더 이상 추상적이지 않다.

예를 들면, 우리는 Person클래스를 상속받고 getDescription메소드를 구현한 Student클래스를 정의할 것이다.
Student클래스의 메소드는 추상적이 아니여서, 추상클래스로서 선언이 필요로 하지 않는다.

클래스는 추상메소드를 가지고 있지 않더라도 abstract로서 선언될 수 있다.

추상클래스는 인스턴스화 될 수 없다.
만약 클래스가 abstract로서 선언된다면, 그것은 생성된 클래스의 객체가 아니다.
예를 들면,
    new Person("Vince Vu")
는 오류이다.
그러나 당신은 구체적인 서브클래스의 객체를 생성할 수 있다.
추상클래스의 object variables를 생성할 수 있다는 것을 명심해라.
그러나 각 변수는 추상적이지 않은 서브클래스의 객체를 참조하여야 한다.
예를 들면,
    Person p = new Student("Vince Vu", "Economics");
여기 p는 비추상적인 서브클래스 Student의 인스턴스를 참조한 Person 추상적 타입의 변수이다.

```
C++ 필기 : C++에서, 추상 메소드는 순수 가상 함수(pure virtual function)이라 불리고, trailing=0과 함께 태그된다. 다음과 같이,

class Person // C++
{
    public:
        virtual string getDescription() = 0;
        ...
};

C++ 클래스는 적어도 하나의 순수 가상 함수를 가지고 있다면  추상적이다.
C++에서 추상클래스를 의미하는 특별한 키워드가 없다.
```

구체적인 Person 추상클래스를 상속받은 Student 서브클래스를 정의해라.

    public class Student extends Person
    {
        private String major;

        public Student(String name, String major)
        {
            super(name);
            this.major = major;
        }

        public String getDescription()
        {
            return "a student majoring in " + major;
        }
    }

Student 클래스는 getDescription 메소드를 정의한다.
그러므로, Student 클래스 안의 모든 메소드는 구체적이고, 그 클래스는 이미 추상클래스가 아니다.

Listing 5.4에서 보여지는 프로그램은 추상클래스 Person과 두 개의 구체적인 , Employee와 Student 클래스를 정의한다.
우리는 employee와 student 객체와 함께 Person 참조의 배열을 채운다:

    Person[] people = new Person[2];
    people[0] = new Employee(...);
    people[1] = new Student(...);

그러면 우리는 이 객체의 이름과 묘사를 출력한다.

    for(Person p : people)
        System.out.println(p.getName() + ", " + p.getDescription());

몇몇 사람들은 p.getDescription() 호출에 의해 당혹스러워 한다.
이 호출이 정의되지 않은 메소드가 아닌가?
Person 추상클래스의 객체를 생성하는 것이 불가능하기 떄문에 변수 p가 Person객체 결코 참조하지 않는다는 것을 명심해라.
변수 p는 항상 Employee 또는 Student와 같은 구체적인 서브클래스의 객체를 참조한다.

당신은 Employee와 Student 서브클래스에서 getDescription메소드를 간단히 정의한, Person 슈퍼클래스로부터 완전히 추상메소드를 생략할수 있었나?
만약 당신이 그렇게 했다면, 변수 p에서 getDescription메소드를 호출할 수 없을것이다.
컴파일러는 당신이 오직 클래스에서 선언된 메소드를 호출한다는 것을 지지한다.

추상메소드는 자바 프로그래밍 언어에서 중요한 개념이다.
당신은 인터페이스안에서 그들을 가장 흔히 마주칠 것이다.
인터페이스에 대한 더 많은 정보를 위해, 6장으로 가라.

```
Listing 5.4 abstractClasses/PersonTest.java

package abstractClasses;

/**
    * This program demonstrates abstract classes.
    * @version 1.01 2004-02-21
    * @author Cay Horstmann
    */
public class PersonTest
{
    public static void main(String[] args)
    {
        Person[] people = new Person[2];

        // fill the people array with Student and Employee objects
        people[0] = new Employee("Harry Hacker", 50000, 1989, 10, 1);
        people[1] = new Student("Maria Morris", "computer science");

        // print out names and descriptions of all Person objects
        for(Person p : people)
            System.out.println(p.getName() + ", " + p.getDescription());
    }
}
```

```
Listing 5.5 abstractClasses/Person.java

package abstractClasses;

public abstract class Person
{
    public abstract String getDescription();
    private String name;

    public Person(String name)
    {
        this.name = name;
    }

    public String getName()
    {
        return name;
    }
}
```

```
Listing 5.6 abstractClasses/Employee.java

package abstractClasses;

import java.time.*;

public class Employee extends Person
{
    private double salary;
    private LocalDate hireDay;

    public Employee(String name, double salary, int year, int month, int day)
    {
        super(name);
        this.salary;
        hireDay = LocalDate.of(year, month, day);
    }

    public double getSalary()
    {
        return salary;
    }

    public LocalDate getHireDay()
    {
        return hireDay;
    }

    public String getDescription()
    {
        return String.format("an employee with a salary of $%.2f", salary);
    }

    public void raiseSalary(double byPercent)
    {
        double raise = salary * byPercent / 100;
        salary += raise;
    }
}
```

```
Listing 5.7 abstractClasses/Student.java

package abstractClasses;

public class Student extends Person
{
    private String major;

    /**
        * @param name the student's name
        * @param major the student's major
        */
    public Student(String name, String major)
    {
        // pass n to superclass constructor
        super(name);
        this.major = major;
    }

    public String getDescription()
    {
        return "a student majoring in " + major;
    }
}
```

---
#### **5-1-10 보호 접근 (Protected Access)**
---

당신도 알다시피, 클래스 안에 필드는 private로 태그되고, 메소드들은 보통 public으로 태그된다.
private로 선언되는 어떤 특징들은 다른 클래스에서 보이지 않는다.
우리가 이 장의 시작 부분에서 말했듯이, 이것은 서브클래스를 위한 진실이다:
서브클래스는 슈퍼클래스의 private필드에 접근할 수 없다.

그러나, 당신이 오직 서브클래스에서 엄격한 메소드를 원하는 순간이 있다. 또는, 덜 흔하게, 서브클래스 메소드가 슈퍼클래스 필드에 접근하는 것을 허락하는 것을 원하는 순간이 있다.
당신은 protected의 특징을 가진 클래스를 선언한다.
예를 들면, 만약 Employee 슈퍼클래스가 private 대신에 protected로서 HireDay필드를 선언한다면, Manager메소드는 직접 접근할 수 있다.

그러나, Manager클래스 메소드들은 다른 Employee객체가 아닌, Manager객체의 HireDay필드에서 peek할 수 있다.
이 제한은 단지 protected필드에 접근하기 위해 서브클래스를 형성함으로써 protected메커니즘을 남용할 수 없도록 만들어진다.

실제는, 주의깊게 protected필드를 사용해라.
당신의 클래스가 다른 프로그래머들에 의해 사용되고, 당신이 protected필드와 함께 설계했다고 가정하자.
당신에게 알려지지 않은, 다른 프로그래머들은 당신의 클래스로부터 클래스를 상속할지도, 당신의 protected필드에 접근하는 것을 시작할지도 모른다.
이 경우에 있어서, 당신은 더 이상 그 프로그래머들을 화나게 하지 않는 이상 당신의 클래스의 구현을 바꿀 수 없다.
그것은 데이터 캡슐화를 권장하는 OOP의 정신에 반하는 것이다.

protected 메소드는 더 이해하기 쉽다.
한 클래스는 만약 사용하기 곤란하다면 protected로서 메소드를 선언할지도 모른다.
이것은 서브클래스(아마 그들의 조상을 잘 아는)는 메소드를 올바르게 사용하는 것이 신뢰될 수 있다는 것을 나타내지만 다른 클래스는 할 수 없다.

메소드 종류의 좋은 예시는 Object클래스의 clone메소드이다.
6장에서 더 자세하게 보자.

```
C++ 필기 : 그것이 일어남으로써, 자바에서 protected특징은 같은 패키지에서 모든 다른 클래스들 뿐만 아니라 모든 서브클래스에서 보일 수 있다.
이것은 C++에서 protected의 의미가 미세하게 다르고, C++보다 덜 안전한 Java에서 protected의 개념을 만든다.
```

여기 시각을 제어하는 자바에서 네 개의 접근 수식어들의 요약이 있다.

1. private - 오직 클래스에서만 보이는
2. public - 전체에서 보이는
3. protected - 패키지와 모든 서브클래스에서 보이는
4. default - 패키지에서 보이는