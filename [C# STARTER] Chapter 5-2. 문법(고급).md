# 정적 선언, 상속

<details>
<summary>1. 정적 선언(static)</summary>
<div markdown="1">       

### 정적 선언(static)은 무엇이고 필요한 이유?
* 이해하기 위해서는 객체들이 언제 메모리에 적재되고 언제 메모리 공간을 반환하는지 알아야 함
  * `정적으로 선언한 객체` : 프로그램이 해당 객체를 처음 호출하는 순간 메모리 공간을 할당받아 프로그램이 끝날 때까지 그 상태를 유지함
  * `동적으로 선언한 객체` : 그것이 사용될 때마다 메모리의 공간을 할당받고 또 역할이 끝나면 곧바로 사용하던 메모리를 시스템에 반환함
 
### 예시 코드
```C#
class TheaterDemo
{
  static void Main()
  {
    do
    {
      Console.Write("영화를 관람하시겠습니까? (y/n): ");
      char getTicket = Convert.ToChar(Console.ReadLine().ToLower());

      if(getTicket == 'y')
      {
        Console.Write("좌석을 선택하세요(1~10번): ");
        int seatNum = Convert.ToInt16(Console.ReadLine());

        //배열은 0~9이기 때문에 1을 빼주고 있다.
        SeatControl.SeatCheck(seatNum - 1);
      }

      else
      { break; }
    } while(true); //getTickey == 'y'가 아닌 경우 반복문을 멈춘다.

    Console.WriteLine("\n금일 총 관람객 수는 {0}명입니다.", TotalNum.GetTotal());
  }
}

class TotalNum
{
  private static int total = 0;

  public static void AddTotal(int n)
  { total += n; }

  public static int GetTotal()
  { return total; }
}

class SeatControl
{
  //배열의 모든 값을 0으로 초기화해준다.
  private static int[] seatTaken = new int[10] { 0, 0, 0, 0, 0, 0, 0, 0, 0, 0 };

  public static void SeatCheck(int x)
  {
    if(SeatTaken[x] == 0)
    {
      //좌석이 배정되면 해당 자리를 1로 바꿔준다.
      seatTaken[x] = 1;

      //좌석번호 1~10과 배열의 주소 0~9를 일치시키기 위해 1를 더해주고 있다.
      Console.WriteLine("{0}번 좌석이 배정되었습니다.", x + 1;);

      //정상적인 좌석 배치가 이루어지면 총 관람객 수에 포함시킨다.
      TotalNum.AddTotal(1);
    }

    else
    {
      //좌석번호 1~10과 배열의 주소 0~9를 일치시키기 위해 1를 더해주고 있다.
      Console.WriteLine("{0}번 좌석의 선택은 불가합니다.", x + 1);
    }
  }
}
```
* 지금까지 클래스를 사용하기 위해서는 클래스의 인스턴스를 생성했어야 했음
* But, 위 코드에서는 클래스에 대한 인스턴스를 만들지 않고 바로 '클래스명.함수명()'의 형태로 클래스와 클래스 안에 있는 함수를 사용하고 있음
* 이처럼 static으로 선언된 객체들은 **인스턴스의 생성없이** 바로 사용해야 한다는 것을 기엉하고 있어야 함
  * why? `정적으로 선언된 객체`들은 메모리에 상주하기 때문에, 사용할 때마다 새로 인스턴스를 생성하지 않고 메모리에서 바로 호출하기 때문임
* static 키워드로 선언하지 않은 모든 객체는 기본적으로 동적으로 간주함 
 
### 정적 선언을 사용할 때 기억해야 할 4가지
* 정적으로 선언한 클래스는 **인스턴스를 생성할 수 없다.** So, <클래스명.객체>의 형태로만 사용할 수 있음
* 정적으로 선언한 클래스는 오직 **정적 객체**만 가질 수 있다.
* 클래스뿐만 아니라 변수, 함수, 프로퍼티, 생성자도 정적으로 선언할 수 있다.
* 정적으로 선언한 객체는 **정적으로 선언한 객체**에서만 호출할 수 있다.

### 코드를 통한 정적 선언 규칙 이해
```C#
static class GetNumber
{
  //오류1 static 클래스 안에서 동적 변수를 사용하고 있다.
  public int num = 10;

  //오류2 static 클래스 안에서 동적 함수를 사용하고 있다.
  public int gtNumber()
  { return num; }
}

class GetNumber2 //동적으로 선언한 클래스
{
  public int num2 = 10; //동적으로 선언한 변수: OK

  public int gtNumber2() //동적으로 선언한 함수: OK
  { return num2; }
}

class Program
{
  static void Main()
  {
    //오류3 static 클래스의 인스턴스를 생성하고 있다.
    GetNumber gt = new GetNumber();

    //오류4 static 클래스의 인스턴스를 사용해 static 클래스 안의 함수를 호출하고 있다.
    Console.WriteLine(gt.gtNumber());

    //static으로 선언한 Main()함수에서 동적 클래스의 인스턴스를 만들고 있다: OK
    GetNumber2 gt2 = new GetNumber2();

    //동적 클래스의 인스턴스를 사용해 static 클래스 안의 함수를 호출하고 있다: OK
    Console.WriteLine(gt2.gtNumber2());
  }
}
```
* 오류 수정 코드
```C#
static class GetNumber
{
  //해결: static 클래스 안에서 static 변수만 사용할 수 있다.
  public static int num = 10;

  //해결: static 클래스 안에서 static 함수만 사용할 수 있다.
  public static int gtNumber()
  { return num; }
}

class Program
{
  static void Main()
  {
    //해결: 인스턴스의 생성없이 바로 함수를 호출한다.
    Console.WRiteLine(GetNumber.gtNumber());
  }
}
```

* 동적으로 선언된 클래스가 정적 변수나 정적 함수를 가질 수 있을까? 가능함
* 또한 동적으로 선언된 객체를 정적으로 선언된 객체에서 호출하는 것도 얼마든지 가능함
* 불가능한 것은 오로지 정적 객체를 동적 객체에서 호출하는 경우뿐임

```C#
class NumClass //동적 클래스
{
  pirvate static int x = 999; //정적 변수: OK

  public static int getNum() //정적 함수: OK
  { return x; }
}

class NumClass2 //동적 클래스
{
  //정적 함수를 호출하여 정적 변수의 값을 배정하고 있다.
  //값을 배정받는 변수 y 역시 static이기 때문에 가능하다.
  private static int y = NumClass.getNum();

  public static int getNum2() //정적 함수
  { return y; }
}

class Program
{
  static void Main()
  {
    //정적 함수를 호출하여 정적 변수(y)에 저장된 값을 출력하고 있다.
    Console.WriteLine(NumClass2.getNum2());
  }
}
```

### 상수는 정적 객체일까?
* 상수는 그 자체로 항상 정적 객체에 속함
* So, static 키워드를 사용하지 않더라도 다른 정적 변수처럼 사용할 수 있음
```C#
class ConstantNumber
{
  public const int NUM = 100;
}

class Program
{
  static void Main()
  {
    Console.Write(ConstantNumber.NUM);
  }
}
```
* 상수로 선언된 변수는 클래스 내에 있는 정적 함수나 변수를 부르는 방법과 같음
* 같은 방법으로 호출이 가능한 이유는 상수가 처음부터 정적 변수이기 때문임
* 같은 이유로 상수에 static 키워드를 사용하는 것은 허용되지 않음
* C#에서는 클래스 전체를 정적으로 선언할 수도 잇음
  * 단, 정적으로 클래스를 선언할 경우 클래스 안에 들어있는 모든 객체 역시 정적으로 선언해야 함
* 정적으로 선언한 객체가 메모리에 머물러 있기 때문에 나타나는 중요한 특징
  * 정적 객체를 여러 곳에서 호출하는 경우에 그 값이 공유된다는 사실!
```C#
//static class StaticCounter 가 아니었음에 주의!
class StaticCounter
{
  public static int count = 0;

  public StaticCounter() //생성자(constructor)
  { count++; }
}

class Program
{
  static void Main()
  {
    StaticCounter stc1 = new StaticCounter();
    StaticCounter stc2 = new StaticCounter();

    Console.WriteLine("StaticCounter.count = {0}", StaticCounter.count);

    /* 두 번에 걸쳐 클래스의 인스턴스 stc1, stc2가 만들어졌으므로
       클래스 생성자는 두 번 작동하게 된다. So, count는 두 번 증가한 값인 2가 된다. */
  }
}
```
</div>
</details>

___

<details>
<summary>2. 상속(inheritance)</summary>
<div markdown="1">       

### 상속의 특징
* **상속(inheritance)** 은 이미 존재하는 다른 클래스를 기반으로 새로운 클래스를 정의할 수 있게 함
* 이미 존재하는 클래스의 기능을 그대로 가져와 사용하기 때문에
  * 불필요한 코드의 중복을 피할 수 있고,
  * 프로그램의 유지 및 보수의 편의성과 정확성을 높여줌
 
### 부모 클래스(base class)와 자식 클래스(derived class)
* 자식 클래스는 부모 클래스에서 선언한 기능들을 다시 선언할 필요 없이 그대로 가져다 쓸 수 있으며,
* 단지 자식 클래스에서 필요한 기능만 추가적으로 선언해서 사용하는 것
* 아무리 자식 클래스라고 해도 부모 클래스에서 'private'으로 선언한 객체들에는 접근할 수 없음

### 예시 코드로 이해하는 상속
```C#
class Person //부모 클래스
{
  public int Age { set; get; }
  public string Name { set; get; }
}

class Student : Person //자식 클래스(Student) : 부모 클래스(Person)
{
  public Student(int age, string name)
  {
    //부모 클래스의 프로퍼티를 아무 제약없이 사용하고 있다.
    Age = age;
    Name = name;
  }
}

class Program
{
  static void Main()
  {
    Console.Write("학생의 나이를 입력하세요: ");
    int age = Convert.ToInt16(Console.ReadLine());

    Console.Write("학생의 이름을 입력하세요: ");
    string name = Console.ReadLine();

    //자식 클래스의 인스턴스를 생성하고 있다.
    Student st = new Student(age, name);

    //자식 클래스의 인스턴스가 부모 클래스의 프로퍼티를 사용하고 있다.
    Console.WriteLine(st.Age);
    Console.WriteLine(st.Name);
  }
}
```

* 하나의 부모 클래스를 기반으로 필요한 만큼의 자식 클래스를 만들 수 있음
```C#
class Person //부모 클래스
{
  public int Age { set; get; }
  public string Name { set; get; }
  public string TelNum { set; get; }
  public string Subject { set; get; }
}

//자식 클래스(Student) : 부모 클래스(Person)
class Student : Person
{
  public Student(int age, string name)
  {
    //부모 클래스의 프로퍼티를 아무 제약없이 사용하고 있다.
    Age = age;
    Name = name;
  }
}

//자식 클래스(Parent) : 부모 클래스(Person)
class Parent : Person
{
  public Parent(string telNum)
  {
    TelNum = temNum;
  }
}

//자식 클래스(HRTeacher) : 부모 클래스(Person)
class HRTeacher : Person
{
  public HRTeacher(string subject, string name)
  {
    Subject = subject;
    Name = name;
  }
}

class Program
{
  static void Main()
  {
    Console.Write("학생의 나이를 입력하세요: ");
    int age = Convert.ToInt16(Console.ReadLine());

    Console.Write("학생의 이름을 입력하세요: ");
    string name = Console.ReadLine();

    //자식 클래스(Student)의 인스턴스를 생성하고 있다.
    Student st = new Student(age, name);

    Console.WriteLine();

    Console.Write("부모님의 전화번호를 \'-\'없이 입력하세요: );
    string tel = Console.ReadLine();

    //자식 클래스(Parent)의 인스턴스를 생성하고 있다.
    Parent pr = new Parent(tel);

    Console.WriteLine();

    Console.Write("담임 선생님의 과목을 입력하세요: ");
    string subject = Console.ReadLine();

    Console.Write("담임 선생님의 이름을 입력하세요: ");
    string hrname = Console.ReadLine();

    //자식 클래스(HRTeacher)의 인스턴스를 생성하고 있다.
    HRTeacher hrt = new HRTeacher(subject, hrname);

    Console.WriteLine();

    //자식 클래스의 인스턴스가 부모 클래스의 프로퍼티를 사용하고 있다.
    Console.WriteLine("{0} 학생은 {1}살입니다.", st.Name, st.Age);
    Console.WriteLine("부모님의 전화번호는 {0}번이고", pr.TelNum);
    Console.WriteLine("담임선생님의 이름은 {0}, 과목은 {1}입니다.", hrt.Name, hrt.Subject);
  }
}
```
* 부모 클래스에서 상속받을 수 있는 것은 프로퍼티에 그치지 않음
* 변수와 함수 그 어떤 것이라도 가져다 쓸 수 있음
* 단, private으로 제한되어 있으면 안 됨
* 부모 클래스로부터 변수와 함수를 상속받아 사용하는 코드 예시

```C#
class Greeting
{
  public string name;

  public void Greet()
  {
    Console.WriteLine("Hello! {0}.", name);
  }
}

class Person : Greeting
{
  public Person(string n)
  {
    //부모 클래스의 변수를 상속받아 사용하고 있다.
    name = n;
  }
}

class Program
{
  static vod Main()
  {
    Console.Write("이름을 입력하세요: ");
    string n = Console.ReadLine();

    //자식 클래스의 인스턴스를 생성한다.
    Person p = new Person();

    //부모 클래스에서 함수를 상속받아 사용하고 있다.
    p.Greet();
  }
}
```
</div>
</details>
