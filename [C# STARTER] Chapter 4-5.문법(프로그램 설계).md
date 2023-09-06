# 생성자와 소멸자

<details>
<summary>1. 생성자(constructor)</summary>
<div markdown="1">       

#### 생성자란?
* 클래스의 인스턴스가 만들어질 때 자동으로 함께 만들어지는 특별한 함수
* 특별한 연산을 포함하는 생성자를 원하는 경우, 개발자가 따로 만들어주어야 함
  
#### 생성자 규칙
* 생성자는 자신이 속한 클래스와 **같은 이름**을 가져야 하며
* 반드시 **public**으로 정의되어야 하며
* **반환자료형을 가질 수 없다.** 심지어는 void도 허용하지 않는다.
* 단, 필요에 따라 **매개변수**를 가질 수 있으며, 오버로딩을 허용한다.

#### 예시 코드
```C#
class BankAccount
{
  /* 생성자는 반환자료형을 갖지 않으며
     오직 접근제한자 public과 생성자 이름만을 가진다. */
  public BankAccount()
  {
    Console.WriteLine("새로운 계좌가 생성되었습니다.");
  }
}

class Program
{
  static void Main()
  {
    Console.Write("새로운 계좌를 개설하시겠습니까? (y/n) ");
    char newAC = char.Parse(Console.ReadLine().ToLower());
    if(newAC == 'y')
    {
      BankAccount acc = new BankAccount(); //인스턴스 생성
    }
  }
}
```
* Main() 함수에서 BankAccount 클래스의 새로운 인스턴스 'acc'가 만들어진 것을 볼 수 있음
* 클래스의 인스턴스를 만들었을 뿐인데, 이 프로그램은 새로운 계좌가 개설되었다는 메시지를 출력할 것
  * BankAccount 클래스는 **생성자**를 포함하고 있으므로 클래스 객체(인스턴스)가 생성됨과 동시에 이 생성자를 실행했기 때문임
* 생성자가 매개변수를 가지고 있다면 클래스의 인스턴스를 생성할 때 이에 대한 인수를 전달해야 함
```C#
class BankAccount
{
  public BankAccount(string name)
  {
    Console.WriteLine("{0}님의 새로운 계좌가 생성되었습니다!", name);
  }
}

class Program
{
  static void Main()
  {
    Console.Write("새로운 계좌를 개설하시겠습니까? (y/n) ");
    char newAC = char.Parse(Console.ReadLine().ToLower());

    Console.Write("이름을 입력하세요: ");
    string cstName = Console.ReadLine();

    if(newAC == 'y')
    {
      // 클래스의 인스턴스를 생성할 때 인수를 함께 전달한다.
      BankAccount acc = new BankAccount(cstName); 
    }
  }
}
``` 
</div>
</details>

___

<details>
<summary>2. 생성자 오버로딩</summary>
<div markdown="1">       

* 같은 이름의 함수를 여러 개 가질 수 있는 것처럼, 같은 이름의 생성자를 여러 개 가질 수도 있음
* 오버로딩이 갖는 장점
  * 다양한 상황에 좀 더 유연하게 대처할 수 있는 프로그램을 만들 수 있다.
* But, 함수와 마찬가지로 시그니처까지 동일한 생성자는 만들 수 없음
* 예시 코드
```C#
class Person
{
  public Person()
  { Console.WriteLine("Hi there!"); }

  public Person(string name)
  { Console.WriteLine("Hi {0}!", name); }

  public Person(string name, int age)
  { Console.WriteLine("Hi {0}! You are {1} years old!", name, age); }
}

class Program
{
  static void Main()
  {
    Person p1 = new Person();
    Person p2 = new Person("James");
    Person p3 = new Person("James", 21);
  }
}
```
</div>
</details>

___

<details>
<summary>3. 소멸자(destructor)</summary>
<div markdown="1">       

#### 소멸자란?
* 소멸자(종료자) 역시 클래스의 쓰임이 다하면 자동으로 생성됨
* 새로운 객체를 만들고 회수하지 않는다면 컴퓨터의 메모리는 감당할 수 없음
* So, 자신의 역할을 다한 객체는 반드시 컴퓨터에 자원을 반환해야 하는데, 이것이 바로 소멸자의 역할!
* C#에서는 강력한 **가비지 수집(garbage collector) 기능**을 제공하여 이러한 역할을 대신하기에, 개발자는 별도의 소멸자를 만들 필요가 없음
* 생성자와 마찬가지로 특별한 역할을 부여하고 싶다면 따로 만들어야 함
  
#### 소멸자 규칙
* 하나의 클래스는 **하나의 소멸자만** 가질 수 있으며, 소멸자는 오직 **클래스에만 적용**된다.
* 소멸자는 사용자가 **직접 호출할 수 없다.** 소멸자는 필요할 때 **스스로 작동**하는 것이다.
* 소멸자는 **접근 제한자**와 **매개 변수**를 가질 수 없다.
* 소멸자는 **상속**이나 **오버로드**가 될 수 없다.
* 소멸자의 이름은 클래스와 같은 이름을 가져야 하며, 이름 앞에 **~**를 붙여줘야 함
  
#### 예시 코드
```C#
class Person
{
  pirvate int a;

  public Person(int a)
  {
    this.a = a;
    Console.WriteLine("{0}번 클래스 객체 생성", this.a);
  }
  ~Person() //소멸자를 따로 만들어주고 있다.
  {
    Console.WriteLine("{0}번 클래스 객체 소멸", a);
  }
}

class Program
{
  static void Main()
  {
    Console.Write("몇 개의 클래스 객체를 만들까요?");
    int x = Convert.ToInt32(Console.ReadLine());

    for(int y = 1; y <= x; y++)
    {
      Person p = new Person(y); //새로운 클래스 인스턴스 생성
    }

    Console.WriteLine();

    GC.Collect();  //가비지 수집을 즉시 수행하도록 강제하고 있다.
  }
}
```
</div>
</details>
