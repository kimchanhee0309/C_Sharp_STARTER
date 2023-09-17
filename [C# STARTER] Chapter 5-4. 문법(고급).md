# 추상 클래스, 인터페이스

<details>
<summary>1. 추상 클래스(abstract class)</summary>
<div markdown="1">       

### 일반적인 상속과의 차이
* 추상으로 선언된 함수는 반드시 자식 클래스에서 함수를 따로 정의해주어야 함
* 또한 해당 자식 클래스는 반드시 `override` 키워드로 선언해야 함

### 추상 클래스의 특징
* 추상으로 선언한 함수를 가지기 위해서는 해당 함수를 포함하는 클래스 역시 추상으로 선언해야 함
* 이때, 추상으로 선언한 함수는 자신만의 연산(명령문)을 가질 필요가 없음
  * why? 자식 클래스에 의해 100% 대체될 것이기 때문에!
* 예시 코드로 이해하는 추상 클래스
```C#
abstract class Maker
{
  public abstract void MadeWhere();

  public void Warehouse()
  {
    Console.WriteLine("상품 등록 완료");
    Console.WriteLine();
  }
}

class Korea : Maker
{
  public override void MadeWhere()
  { Console.WriteLine("국산입니다."); }
}

class China : Maker
{
  public override void MadeWhere()
  { Console.WriteLine("중국산입니다."); }
}

class Program
{
  static void Main()
  {
    Maker k = new Korea();
    k.MadeWhere();
    k.Warehouse();

    Maker c = new China();
    c.MadeWhere();
    c.Warehouse();
  }
}
```

### 추상 클래스가 존재하는 이유와 특징
* 추상 클래스가 존재하는 이유
  * **강제성**을 부여하기 위해서
  * 상속과 추상 클래스를 사용하면 코드 작성의 **틀**을 강제할 수 있음
  * 다시 말해, 추상 클래스는 실제 연산의 기능을 가지지는 않지만, 코딩하는 데 있어 일정한 양식을 제시하기 위해 사용함
* 추상 클래스의 특징
  * 추상 클래스는 `static`이나 `virtual` 키워드를 사용할 수 없다.
  * 추상 클래스는 Maker m = new Maker() 처럼 **자기 자신의 인스턴스**를 생성할 수 없다.
  * 추상 메소드는 접근제한자를 **private**으로 선언할 수 없다.
  * 추상 메소드는 **개별 연산**을 수행할 수 없다. But, 추상이 아닌 메소드는 가질 수 있다.
</div>
</details>

___

<details>
<summary>2. 인터페이스(interface)</summary>
<div markdown="1">       

### 인터페이스(interface)란?
* 추상 클래스보다 높은 수준의 추상 멤버로만 구성된 클래스를 말함
* 클래스를 인터페이스로 선언하면 이에 속한 모든 멤버들은 별도의 선언이 없이도 **추상의 속성**을 가지게 되며, 모두 public으로 간주함
  * 추상의 속성을 가진다는 것은 개별적인 연산을 수행할 수 없다는 말!
  * 즉, 인터페이스로 정의한 클래스의 모든 멤버는 어떤 기능도 가질 수 없음
* 즉, 클래스 밖에서도 얼마든지 호출이 가능하다는 뜻임
* But, 함수, 프로퍼티, 인덱서 등 모든 것을 가질 수 있지만, **변수는 가질 수 없다**.

### 추상 클래스와 다른 점
* 자식 클래스에 override 키워드를 사용하지 않는다는 점

### 인터페이스가 존재하는 이유?
* **양식의 강제성**을 부여하기 위해서!

### 예시를 통해 이해하는 인터페이스
* 인터페이스를 정의할 때 접근 제한자 public은 써도 되고 생략해도 됨
* But, override 키워드는 사용할 수 없음
```C#
interface IMaker  //public interface IMaker 이라고 선언해도 된다.
{
  //public void MadeWhere()라고 선언해도 된다.
  void MadeWhere();

  //public void Warehouse()라고 선언해도 된다.
  void Warehouse();
}

class Korea : IMaker
{
  //override void MadeWhere() 이라고 선언할 수 없다.
  public void MadeWhere()
  { Console.WriteLine("국산입니다"); }

  public void Warehouse()
  { Console.WriteLine("상품 등록 완료\n"); }
}

class China : IMaker
{
  //override void MadeWhere() 이라고 선언할 수 없다.
  public void MadeWhere()
  { Console.WriteLine("중국산입니다"); }

  public void Warehouse()
  { Console.WriteLine("상품 등록 완료\n"); }
}

class Program
{
  statice void Main()
  {
    IMaker k = new Korea();
    k.MadeWhere();
    k.Warehouse();

    IMaker c = new China();
    c.MadeWhere();
    c.Warehouse();
  }
}
```

### 다중 상속
* 일반적인 상속은 하나의 부모 클래스에 여러 자식 클래스가 존재할 수 있지만, 하나의 자식 클래스에 여러 부모 클래스가 존재할 수는 없었다.
* But, 인터페이스를 이용하면 하나의 자식 클래스가 여러 부모 클래스로부터 상속받을 수 있다. 이를 **다중 상속**이라고 함
* 다중 상속을 구현하는 방법
  * 자식 클래스를 선언할 때 클래스의 이름 옆에 상속받을 부모 클래스를 콤마(.)로 열거해 주면 됨
```C#
interface IMaker
{
  void MadeWhere();
  void Warehouse();
}

interface IOwner
{
  void WhoOwns();
  void Customs();
}

//하나의 자식 클래스가 두 개의 부모 클래스로부터 상속을 받고 있다.
class Korea : IMaker, IOwner
{
  public void MadeWhere()
  { Console.WriteLine("국산입니다"); }

  public void Warehouse()
  { Console.WriteLine("상품 등록 완료"); }

  public void WhoOwns()
  { Console.WriteLine("대한민국 회사 제품입니다"); }

  public void Customs()
  { Console.WriteLine("관세 납부 완료"); }
}

//하나의 자식 클래스가 두 개의 부모 클래스로부터 상속을 받고 있다.
class China : IMaker, IOwner
{
  public void MadeWhere()
  { Console.WriteLine("중국산입니다"); }

  public void Warehouse()
  { Console.WriteLine("상품 등록 완료"); }

  public void WhoOwns()
  { Console.WriteLine("일본 회사 OEM 제품입니다"); }

  public void Customs()
  { Console.WriteLine("관세 납부 완료"); }
}

class Program
{
  static void Main()
  {
    IMaker km = new Korea();
    IOwner ko = new Korea();
    km.MadeWhere();
    km.Warehouse();
    ko.WhoOwns();
    ko.Customs();

    IMaker cm = new China();
    IOwner co = new China();
    cm.MadeWhere();
    cm.Warehouse();
    co.WhoOwns();
    co.Customs();
  }
}
```
* 인터페이스를 사용하면 하나의 자식 클래스가 둘 이상의 부모 클래스에게 상속을 받을 수 있음
* 이러한 다중 상속의 허용은 프로그램의 설계에 있어서 더 많은 유연성을 보장해줌
</div>
</details>
