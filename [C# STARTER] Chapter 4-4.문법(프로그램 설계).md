# 프로퍼티(속성), this 키워드

<details>
<summary>프로퍼티(속성)</summary>
<div markdown="1">       

#### 프로퍼티
* 캡슐화해줘야 하는 변수의 수가 많을 때는 캡슐화에 대해 고민을 해야함
  * 각각의 변수마다 이에 접근하기 위한 함수를 따로 구성한다는 것은 번거로운 작업이기 때문에
  * So, 좀 더 쉬운 캡슐화 방법이 필요한데, 이러한 문제 해결을 위해 도입된 것이 **프로퍼티(proterty, 속성)**
* 즉, 클래스에 속한 변수의 캡슐화를 쉽고 간편하게 하는 방법이 바로 **프로퍼티**!
  * 이것을 가능하게 하는 키워드를 `접근자(accessor)` 라고 부름
  * 접근자의 종류
    * `set 접근자(setter)` : 쓰기 담당
    * `get 접근자(getter)` : 읽기 담당
* 프로퍼티 선언 시 주의 사항 3가지
  * 프로퍼티는 외부에서 접근할 수 있어야 하므로 반드시 **public으로 선언**해야 함
  * 프로퍼티를 선언할 때는 일반적인 함수와 달리 **이름 뒤에 괄호()를 붙이지 않는다.**
  * 프로퍼티의 이름은 자유롭게 정할 수 있지만, 관례적으로 private으로 선언한 변수와 같은 이름을 사용하되 PascalCase로 적어준다.
* 예시 코드 1
```C#
class Person
{
  private string name = "James";

  public string Name //프로퍼티 선언
  {
    set { name = value; } //setter
    get { return name; } //getter
  }
}
```
* 'value'는 단순한 변수값이 아님
  * `set 접근자`에 사용하는 특별한 키워드이기 때문에, 따로 정의해주지 않아도 됨
* 앞 코드처럼 프로퍼티를 정의하고 나면, 어디서든 private 데이터에 접근하여 값을 수정할 수 있음

* 예시 코드 2
```C#
class Person
{
  private string name = "James";

  public string Name //프로퍼티 선언
  {
    set { name = value; } //setter
    get { return name; } //getter
  }
}

class Program
{
  static void Main()
  {
    //프로퍼티를 사용하기 위해서는 먼저 클래스의 인스턴스를 생성해야 한다.
    Person p = new Person();

    p.Name = "Bob"; //private으로 정의된 변수(Name)의 값을 바꾸고 있다.

    Console.WriteLine("안녕하세요. " + p.Name + "씨!");
  }
}
```
* 예시 코드 3
```C#
class Person
{
  private string name = "James";

  public void setName(string userName) //일반적인 함수 선언
  { name = userName; }

  public string getName() //일반적인 함수 선언
  { return name; }
}

class Program
{
  static void Main()
  {
    Person p = new Person();

    p.setName("Bob");

    Console.WRiteLine("안녕하세요." + p.getName() + "씨!");
  }
}
```
* 예시 코드 2처럼 프로퍼티를 사용하는 경우
  * 선언 자체가 단순하기도 하지만 프로퍼티를 통한 입출력에서도 'p.Name'이라고만 적어주면 됨
* 예시 코드 3처럼 일반 함수를 사용하는 경우
  * setName()과 getName() 두 개의 서로 다른 함수를 정의해야 하며,
  * 사용할 때 역시 'p.setName()', 'p.getName()'이라고 서로 다르게 적어주어야 함
* 예시 코드 4
```C#
class Person
{
  private string name;
  private int age;

  public string Name
  {
    set
    {
      if(value.Length == 0)
      {
        throw new ArgumentException("이름이 입력되지 않았습니다.");
      }

      else
      { name = value; }
    }

    get
    { return name; }
  }

  public int Age
  {
    set
    { age = value; }

    get
    {
      if(age <= 0)
      {
        throw new ArgumentException("나이의 입력이 올바르지 않습니다.");
      }

      else
      { return age; }
    }
  }
}

class Program
{
  static void Main()
  {
    Person p = new Person();

    Console.Write("이름을 입력하세요: ");
    p.Name = Console.ReadLine();

    Console.Write("나이를 입력하세요: ");
    p.Age = Convert.ToInt32(COnsole.ReadLine());

    Console.WriteLine("안녕하세요. {0}씨", p.Name);
    Console.WriteLine("당신의 나이는 {0}살이군요.", p.Age);
  }
}
```
* 프로퍼티 안에서도 일반 함수처럼 다양한 명령문을 사용할 수 있음

#### 자동 구현 프로퍼티(auto implemented property)
```C#
class Person
{
  public string Name
  { set; get; }
}
```
* 자동 구현 프로퍼티를 사용함으로써 'private string name'이라고 따로 변수를 선언하지도 않았다는 사실에 주목
* 아래 코드는 위 코드와 똑같은 작업을 수행함
```C#
class Person
{
  //일반적인 경우 private으로 정의되는 변수를 따로 만들어줘야 함
  private string name;

  public string Name
  {
    set { name = value; }
    get { return name; }
  }
}
```
* 자동 구현 프로퍼티를 사용할 때도 변수의 기본값을 설정할 수는 있음
  * 기본값 설정 방법
```C#
class Person
{
  public string Name { set; get; } = "James"
}
```
* 자동 구현 프로퍼티 예시
```C#
class Person
{
  //자동 구현 프로퍼티 선언
  public string Name { set; get; } = "James";
}

class Program
{
  static void Main()
  {
    Person p = new Person();

    p.setName("Bob"); //private으로 정의된 변수(Name)의 값을 바꾸고 있다.

    Console.WRiteLine("안녕하세요." + p.getName() + "씨!");
  }
}
```
</div>
</details>

___

<details>
<summary>this 키워드</summary>
<div markdown="1">       

* 클래스에서 선언한 멤버 변수와 함수의 매개변수는 같은 이름을 가질 수 있음
  * 어떤 매개변수와 멤버 변수가 상호 작용하는지 알아보기 쉽다는 장점
  * 같은 이름을 가진 두 개의 변수가 존재한다는 것은 코드를 읽기 불편하게 만들 수 있음
* 이런 단점을 극복하는 방법이 **this 키워드**임
  * 즉, 클래스의 멤버버 변수 앞에 `this.` 라고 적어줌으로써 함수의 매개변수와 구별이 되도록 하는 것
```C#
class BankAccount
{
  private double money = 0;

  public void Deposit(double money)
  { this.money += money; }

  public void Withdraw(double money)
  { this.money -= money; }

  public double GetBalance()
  { return this.money; }
}
```
* money라는 멤버 변수 이름과 매개변수 이름이 똑같은 점을 알 수 있음
* this 키워드를 사용하여 어느 것이 멤버 변수이고 매개변수인지 쉽게 구별 가능함
  * this는 멤버 변수 앞에 붙임
</div>
</details>
