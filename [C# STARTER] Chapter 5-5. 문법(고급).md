# 구조체, 델리게이트

<details>
<summary>9. 구조체(struct)</summary>
<div markdown="1">       

### 구조체란?
* 구조체는 클래스가 아닌 **자료형**으로, **변수들을 한데 묶어 캡슐화**한 것임
* So, 클래스보다는 기능이 제한적일 수밖에 없음
  * 구조체는 상속할 수 없고, virtual 함수와 매개 변수를 가지지 않는 **생성자**를 가질 수 없음
* But, 클래스가 아니기 때문에 사용하기 전에 인스턴스를 생성할 필요가 없다는 점은 편리함

### 예시 코드로 이해하는 구조체
```C#
struct School
{
  public string schName;
  public string stName;
  public int stGrade;
}

class Program
{
  static void Main()
  {
    //School sc = new School()이 아니었다는 사실을 기억하기!
    //즉, 변수명의 선언처럼 별도의 인스턴스를 생성없이 사용한다.
    School sc;
    sc.schName = "레이크사이드 고등학교";
    sc.stName = "빌 게이츠";
    sc.stGrade = 3;

    Console.WriteLine("{0} 학생은 {1} {2}학년입니다.", sc.stName, sc.schName, sc.stGrade);
  }
}
```
* 구조체는 기본적으로 **변수의 집합**임
  * So, 변수 이상의 멤버를 포함하는 경우에는 구조체가 아닌 클래스로 구현하는 것이 일반적!
 
```C#
struct Coordinates
{
  public int x;
  public int y;

  //구조체가 자신만의 생성자를 포함하고 있다.
  public Coordinates(int x, int y)
  {
    this.x = x;
    this.y = y;
  }
}

class Program
{
  static void Main()
  {
    Console.Write("X 값: ");
    int x = Convert.ToInt32(Console.ReadLine());

    Console.Write("Y 값: ");
    int y = Convert.ToInt32(Console.ReadLine());

    //구조체가 변수 이상의 멤버를 가진 경우 인스턴스를 생성해야 한다.
    Coordinates c = new Coordinates(x, y);

    Console.WriteLine("좌표값은 ({0}, {1})입니다.", c.x, c.y);
  }
}
```
* 구조체에 포함된 변수만 사용할 때와 달리, 클래스의 생성자를 함께 사용하는 경우에는 앞에서처럼 인스턴스를 생성해주어야 함

### 구조체 vs 클래스
* 구조체는 기본적으로 **값에 대한 참조**이기 때문에 빠ꇸ고 가벼움
* So, 오직 값에 대한 저장과 참고를 목적으로 할 때는 **구조체**를 사용
* 특정 복잡한 연산이나 자료를 다루는 것을 목적으로 할 때는 **클래스**를 사용하는 것이 바람직함
</div>
</details>

___

<details>
<summary>10. 델리게이트</summary>
<div markdown="1">       

### 델리게이트(delegate)란?
* 함수를 담는 변수, 즉 함수 자체를 저장할 때 쓰임
* 하나의 델리게이트는 필요에 따라 여러 함수를 담을 수 있어 편리함

### 델리게이트 사용 규칙
* 델리게이트를 사용하는 함수는 **public**으로 선언되어야 함
* 델리게이트의 반환자료형은 자신이 대리하려는 **함수의 반환자료형과 같아야 함**
* 델리게이트가 매개변수를 가지면 이는 대리하려는 함수의 매개변수와 같은 형식이어야 함. 즉, 대리하려는 함수가 매개변수를 가지지 않으면 델리게이트 역시 매개변수를 가질 수 없음
* 선언된 델리게이트 형식
  >델리게이트명 델리게이트변수명 = <클래스명.함수명>;
  >
  >델리게이트변수명(매개변수);

### 예시코드로 이해하는 델리게이트(delegate)
```C#
using System;

namespace DelegateDemo_1
{
  //델리게이트에서 사용할 클래스와 함수 선언
  class Print
  {
    public void PrintOut(string str)
    {
      Console.WriteLine(str);
    }
  }

  //델리게이트 선언
  delegate void PrintDelegate(string str);

  class Program
  {
    static void Main()
    {
      /* 코딩 순서
         (1) 함수를 사용하기 전에 함수를 가진 클래스의 인스턴스 생성
         (2) 델리게이트의 객체 생성
         (3) 델리게이트 호출
      */

      Print p = new Print();
      PrintDelegate pdg = p.PrintOut;
      pdg("델리게이트 호출 성공!");
    }
  }
}
```
* 하나의 함수를 대리하기 위해 델리게이트를 사용하는 것은 코드의 작성을 어렵게 만들 뿐 별 도움이 되지 않음
* But, 여러 개의 함수를 하나의 델리게이트로 호출해서 사용하는 경우에는 상황이 달라짐

### 멀티케스트 델리게이트(multicast delegate)
* 멀티케스트 델리게이트를 사용하고자 하는 모든 함수는 똑같은 파라미터의 구성(시그니처)을 가져야 하고,
* 같은 구조를 가지는 함수라면 어떤 함수라도 하나의 델리게이트로 호출할 수 있음
* 예시 코드
```C#
using System;

namespace DelegateDemo_2
{
  //델리게이트에서 사용할 클래스와 함수 선언
  class Print1
  {
    public void PrintOut1(string str)
    {
      Console.WriteLine("PrintOut1: " + str);
    }

    public void PrintOut2(string str)
    {
      Console.WriteLine("PrintOut2: " + str);
    }
  }

  //델리게이트에서 사용할 또 다른 클래스와 함수 선언
  class Print2
  {
    public void PrintOut3(string str)
    {
      Console.WriteLine("PrintOut3: " + str);
    }
  }

  //델리게이트를 한번만 선언
  delegate void Printdelegate(string str);

  class Program
  {
    static void Main()
    {
      /* 코딩 순서
         (1) 함수를 사용하기 전에 함수를 가진 클래스의 인스턴스 생성
         (2) 델리게이트의 객체 생성
         (3) 델리게이트 호출
      */

      Print1 p1 = new Print1();

      //델리게이트 선언은 단 한 번만 이루어진다.
      PrintDelegate pdg = p1.PrintOut1;

      pdg("델리게이트1 호출 성공");

      //델리게이트 pdg에 다른 함수를 값으로 전달하고 있다.
      pdg = p1.PrintOut2;
      pdg("델리게이트2 호출 성공");

      //PrintOut3는 다른 클래스에 있음으로 또 다른 인스턴스 생성
      Print2 p2 = new Print2();

      //델리게이트를 따로 선언하지 않은 채 재사용하고 있다.
      pdg = p2.PrintOut3;
      pdg("델리게이트3 호출 성공");
    }
  }
}
```
* 델리게이트를 사용할 때 가장 큰 이점은 이를 통해 **함수 자체를 캡슐화**할 수 있다는 점!
</div>
</details>
