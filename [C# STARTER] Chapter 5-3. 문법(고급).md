# 접근 제한자 protected, 다형성

<details>
<summary>1. 접근 제한자 protected</summary>
<div markdown="1">       

### private과의 차이
* private이 모든 외부의 접근을 차단한다면,
* protected로 선언한 객체는 **자식 클래스를 제외**한 외부의 접근을 차단하는데 사용함
* 즉, protected는 상속과 관련된 특별한 접근 제한자임

### 예시 코드를 통해 이해하기
```C#
class Greeting
{
  protected string name1;
  private string name2;
  public string name3;

  public void Greet1()
  {
    Console.WriteLine("Hello! {0}.", name1);
  }

  public void Greet2()
  {
    Console.WriteLine("Hello! {0}.", name2);
  }

  public void Greet3()
  {
    Console.WriteLine("Hello! {0}.", name3);
  }
}

class Person : Greeting
{
  public Person(string n)
  {
    this.name1 = n; //부모 클래스의 protected 변수를 상속받아 사용하고 있다.
    this.name2 = n; //부모 클래스의 private 변수를 상속받아 사용하고 있다.
    this.name3 = n; //부모 클래스의 public 변수를 상속받아 사용하고 있다.
  }
}

class Program
{
  static void Main()
  {
    Console.WriteL("이름을 입력하세요: ");
    string n = Console.ReadLine();

    Person p = new Person(n); //자식 클래스의 인스턴스를 생성한다.

    p.Greet1();  //부모 클래스에서 protected 변수를 포함한 함수를 상속받아 사용하고 있다.
    p.Greet2();  //부모 클래스에서 private 변수를 포함한 함수를 상속받아 사용하고 있다.
    p.Greet3();  //부모 클래스에서 public 변수를 포함한 함수를 상속받아 사용하고 있다.
  }
}
```
* 앞 코드에서 protected와 public으로 선언한 변수에 대한 상속은 가능하지만,
* private으로 선언한 변수에 대한 상속은 가능하지 않기 때문에 컴파일 오류가 발생함
* So, Greet2()와 name2를 사용하는 부분을 모두 삭제해야만 정상적인 컴파일이 가능함
</div>
</details>

___

<details>
<summary>2. 다형성</summary>
<div markdown="1">       

### 다형성(polymorphism)이란?
* 무언가를 여러 형태로 만드는 기능을 제공함
* 클래스 간의 계급이 존재할 때 즉, 부모-자식 클래스로 상속의 구조를 가질 때 발생함
* 특히 하나의 부모 클래스가 여러 개의 자식 클래스를 가질 때 필요함
* 공통된 부분은 부모 클래스에 구현하고, 이를 모든 자식 클래스에서 상속하도록 한 뒤에 각각의 자식 클래스는 각자 필요한 기능만 구현하도록 만드는 것

### 다형성이 사용되는 2가지 경우
* 상속의 성격은 유지하지만, 각각의 자식 클래스에서 **이와 다른 기능을 수행**하고자 할 때(virual-override)
* 모든 자식 클래스에서 필요로 하는 기능을 **부모 클래스에서 구현**하고, 자식 클래스들은 **각자 필요에 따라 이를 활용**하도록 만들 때(base)

### 다형성을 쓰는 방법과 예시
* 부모 클래스에서 공통분모로 사용되는 객체에는 `'virtual' 키워드`를 사용하고, 이를 물려받는 자식 클래스에는 `'override' 키워드`를 사용함
* 예시 코드
```C#
class Drawing
{
  public virtual void Draw()
  {
    Console.WriteLine("동그라미를 그립니다.");
  }
}

class Triangle : Drawing
{
  public override void Draw()
  {
    Console.WriteLine("세모를 그립니다.");
  }
}

class Rectangle : Drawing
{
  public override void Draw()
  {
    Console.WriteLine("네모를 그립니다.");
  }
}

class Program
{
  static void Main()
  {
    //부모 클래스를 그대로 상속 받아 사용하고 있다.
    Drawing d = new Drawing();
    d.Draw();

    //상속을 받았지만, 자식 클래스의 인스턴스를 생성하고 있다.
    Drawing t = new Triangle();
    t.Draw();  //자식 클래스(Triangle)에서 제공하는 함수를 실행한다.

    //상속을 받았지만, 자식 클래스의 인스턴스를 생성하고 있다.
    Drawing r = new Rectangle();
    r.Draw();  //자식 클래스(Rectangle)에서 제공하는 함수를 실행한다.
  }
}
```
* 인스턴스를 생성할 때 클래스의 이름(Drawing)과 생성하려는 인스턴스의 이름(Triangle)이 서로 다름
  * 이렇게 함으로써 실제 생성되는 인스턴스는 부모 클래스의 객체가 아닌 자식 클래스(Triangle)의 객체가 됨
  * So, 't.Draw()'를 통해 호출되는 함수는 부모 클래스의 Draw()가 아닌 자식 클래스의 Draw()인 것!
  * 즉, 키워드 `virtual`과 `override`에 의해 부모 클래스에 존재하던 Draw() 함수를 자식 클래스의 Draw() 함수가 덮어쓴 것
* But, 부모 클래스에서 정의한 함수 Draw() 역시 그 기능을 상실하지 않는다는 점도 기억해야 함
* 이와 달리 부모 클래스의 기능을 유지하면서 자식 클래스마다 독특한 연산을 추가하는 것도 가능함
  * `base 키워드`를 사용하여 가능함
  * 예시 코드
```C#
class TrafficLight
{
  protected int second;

  public virtual void GetSecond()
  {
    second = DateTime.Now.Second;  //시스템 시계에서 '초' 정보를 가져온다.
    Console.Write(second + "초 입니다, ");
  }
}

class GoStringt : TrafficLight
{
  public override void GetSecond()
  {
    base.GetSecond();

    if(second >= 0 && second <= 19)
    { Console.WriteLine("직진하세요!"); }

    else
    { Console.WriteLine("직진을 하지 마세요!"); }
  }
}

class TurnRight : TrafficLight
{
  public override void GetSecond()
  {
    base.GetSecond();

    if(second >= 20 && second <= 39)
    { Console.WriteLine("우회전을 하세요!"); }

    else
    { Console.WriteLine("우회전을 하지 마세요!"); }
  }
}

class TurnLeft : TrafficLight
{
  public override void GetSecond()
  {
    base.GetSecond();

    if(second >= 40 && second <= 60)
    { Console.WriteLine("좌회전을 하세요!"); }

    else
    { Console.WriteLine("좌회전을 하지 마세요!"); }
  }
}

class Program
{
  static void Main()
  {
    TrafficLight light1 = new GoStringt();
    light1.GetSecond();

    Console.WriteLine();

    TrafficLight light2 = new TurnRight();
    light2.GetSecond();

    Console.WriteLine();

    TrafficLight light3 = new TurnLeft();
    light3.GetSecond();
  }
}
```
* 부모 클래스에서 가져온 정보를 변형없이 유지하기 위해 `'base.GetSecond()'`를 사용하고 있는 점 기억하기
</div>
</details>
