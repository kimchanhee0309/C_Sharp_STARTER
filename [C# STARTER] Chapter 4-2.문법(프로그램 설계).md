# 클래스, 지역 변수와 전역 변수

## 클래스

* 각각의 프로그램은 각자의 상황에 따라 필요한 데이터를 저장하고 각각의 필요에 따라 이를 가공할 수 있어야 함
* 이를 위해 존재하는 것이 `클래스(class)`
  * 기본적인 연산과 구성 요소를 저마다의 필요한 조합으로 묶어 `클래스`라는 이름으로 사용하는 것
* 클래스 정의 약식
```C#
class <클래스 이름>
{
  statement(s);
}
```
* 정의된 클래스를 사용하기 위해 클래스의 객체를 생성하는 행위를 `인스턴스 생성(instantiation)`이라고 부름
> 클래스명 인스턴스명 = new 클래스명();
```C#
class Student
{
  //클래스 안에는 함수든, 변수든 필요에 따라 다양하게 조합할 수 있다.
  public void SayHi(string name)
  {
    Console.WriteLine("{0} 학생, 반가워요!", name);
  }
}

class Program
{
  static void Main()
  {
    Console.Write("이름을 입력하세요: ");
    string stName = Console.ReadLine();

    //인스턴스 생성
    Student std = new Student();

    //인스턴스를 생성하고 나면, 클래스 안에 정의된 함수를 사용할 수 있다.
    std.SayHi(stName);
  }
}
```
* 객체지향 프로그래밍 언어에서 클래스는 하나의 자료형으로 간주함
  * So, 클래스를 선언할 때도 앞 코드에서처럼 'Student std' 즉, <클래스명 인스턴스명>의 형태로 선언해야 함
  * 이때, 클래스의 이름이 곧 자료형의 이름처럼 사용되는 것!
* 클래스 안에 있는 함수를 사용하기 위해선 클래스에 대한 인스턴스를 만들어주어야 함
  * 인스턴스를 만든 후 `인스턴스 이름.함수명()`의 형태로 클래스 안의 함수를 사용할 수 있음
* 클래스 vs 메소드
  * 클래스 : 다양한 기능을 묶어주는 상위 개념
  * 메소드(함수) : 각각의 기능을 구현하는 하위 개념
* 필드 vs 메소드
  * 필드(feild) : 클래스 안에 사용한 **변수**
  * 메소드 : 클래스 안에 정의된 **함수**    
___

## 지역 변수와 전역 변수

* **지역 변수(local variable)** : 하나의 함수 안에서만 유효한 변수, 자신을 사용하는 함수 안에서 선언
* **전역 변수(global variable)** : 같은 클래스 범위 안의 모든 연산에서 사용할 수 있는 변수, 모든 함수의 밖에서 선언
```C#
static string name = "James"; //전역 변수

static void ShowName()
{
  string name = "Richard"; //지역 변수
  //지역변수(Richard)를 출력할 것이다.
  Console.WriteLine("I am {0}", name);
}

static void Main()
{
  //ShowName() 함수 안의 지역 변수를 호출
  ShowName();

  //ShowName() 함수 안의 지역 변수를 호출 불가,
  //따라서 아래 명령문은 전역 변수(James)를 출력할 것이다.
  Console.WriteLine("I am {0}", name);
}
```
* 지역 변수는 반드시 값을 배정한 뒤에만 사용할 수 있음
* 전역 변수는 배정된 값이 없어도 오류를 일으키지 않음
```C#
//전역 변수 num과 str에 값이 배정되어 있지 않다.
static int num;
static string str;

static void PrintVars()
{
  //지역 변수는 값을 배정하지 않은 상태로 사용할 수 없다.
  int num = 100;
  string str = "James";

  //지역 변수의 출력
  Console.WriteLine("num = {0}\nstr = {1}", num, str);
}

static void Main()
{
  PrintVars();

  /*전역 변수의 출력 : 값이 배정되어 있지 않다.
    그럼에도 오류가 발생하지는 않는다. */
  Consloe.WriteLine("num = {0}\nstr = {1}", num, str);
}
```
