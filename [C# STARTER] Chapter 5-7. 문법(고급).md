# 암시적 변수 선언, 서식 문자열

<details>
<summary>13. 암시적 변수 선언</summary>
<div markdown="1">

### var 키워드
* 명시적 선언(explicit declaration)
  * 변수의 자료형을 먼저 선언한 후, 맞는 값을 배정
> int num1 = 10;

* 암시적 선언(implicit declaration)
  * 입력되는 값에 따라 자료형이 결정됨
  * 이를 위해 사용하는 키워드가 'var' 임
> var num2 = 10;

* 'var' 키워드 사용 시 제약
  * **지역 변수에만 사용** 할 수 있으며, 전역 변수에는 사용할 수 없음
  * 변수를 선언하는 시점에 값을 배졍해야 함
  * 한 번 자료형이 결정된 이후에는 **다른 자료형으로 바꿀 수 없음**
  * 함수의 **반환값** 이나 **매개변수** 에는 사용할 수 없음
  * null 값을 가질 수 없음

* var 사용 시 주의사항 예시 코드
```C#
class ClassA
{
  var a = 10; //오류 : 전역 변수에 사용할 수 없음

  public var Add(int b) //오류 : 반환자료형으로 사용할 수 없음
  {
    var c; //오류 : 선언과 동시에 값을 배정해야 함
    c = a + b;
    return c;
  }
}

class ClassB
{
  public void PrintVar(var d) //오류 : 함수의 매개변수에 사용할 수 없음
  {
    Console.WriteLine(d);
  }
}

class ClassC
{
  public string AddVars(int e, int f)
  {
    var g = e + f; //오류 : 정수값을 배정했기 때문에 g 역시 정수형으로 지정됨
    g = "James M."; //오류 : 자료형이 결정된 이후에 다른 형태의 자료를 입력할 수 없음
    return g;
  }
}
```

* var 예시 코드
```C#
static void Main()
{
  //일반적인 리스트의 선언
  SortedList<int, string> sl_1 = new SortedList<int, string>();

  sl_1.Add(1, "Wozniak");
  sl_1.Add(2, "De Anza");
  sl_1.Add(3, "Berkeley");

  //var 키워드를 이용한 리스트의 선언
  var sl_2 = new SortedList<int, string>();
  sl_2.Add(1, "Jobs");
  sl_2.Add(2, "De Anza");
  sl_2.Add(3, "Reed");

  //반복문의 카운터 변수로 사용하고 있다.
  for (var i = 0; i < sl_2.Count; i++)
  {
    Console.WriteLine(sl_2.Keys[i] + " " + sl_2.Values[i]);
  }
}
```

### 익명 타입
* 하나의 객체가 여러 다른 형태의 자료를 가진 경우, 이를 정의할 수 있는 자료형이 존재하지 않기 때문에 'var'을 사용할 수밖에 없음
* 가장 대표적인 경우가 **익명 타입(anonymous type)** 임.
* 익명 타입 : 읽기 전용, 즉 한 번 배정된 값은 수정할 수 없다는 뜻임
> var 익명타입명 = new { 변수명1 = 값1, 변수명2 = 값2, ... 변수명n = 값n }
* 익명 타입의 변수들은 프로퍼티처럼 사용하게 됨
* 예시 코드
```C#
static void Main()
{
  //익명 타입 선언
  var a = new { Name = "James", Age = 35, EyeSight = 0.8 };

  //익명 타입 호출
  Console.WriteLine("이름 = {0}", a.Name);
  Console.WriteLine("나이 = {0}", a.Age);
  Console.WriteLine("언어 = {0}", a.EyeSight);

  Console.WriteLine();

  Console.Write("이름을 입력하세요: ");
  string x = Console.ReadLine();

  Console.Write("나이를 입력하세요: ");
  int y = int.Parse(Console.ReadLine());

  Console.Write("시력을 입력하세요: ");
  double z = double.Parse(Console.ReadLine());

  //익명 타입 선언
  var b = new { Name = x, Age = y, EyeSight = z };

  //익명 타입 호출
  Console.WriteLine("이름 = {0}", b.Name);
  Console.WriteLine("나이 = {0}", b.Age);
  Console.WriteLine("언어 = {0}", b.EyeSight);

  Console.WriteLine();

  //각각의 자료형 확인
  Console.WriteLine(b.GetType());
  Console.WriteLine(b.Name.GetType());
  Console.WriteLine(b.Age.GetType());
  Console.WriteLine(b.EyeSight.GetType());
}
```
* 익명 타입을 사용하면 **여러 종류의 자료를 하나의 변수로 관리** 할 수 있음
* But, 이를 위해 정의할 수 있는 새로운 자료형이 필요한데, 이때 필요한 키워드가 'var'

### dynamic 키워드(동적 변수)
* 'var' 키워드 단점
  * 선언 시점에 값을 배정해야 함
  * 최초에 배정된 값과 다른 형태의 값을 배정할 수 없음
  * 이러한 불편함을 해결하기 위해 동적 변수인 dynamic이 도입됨

* 'dynamic'이란?
  * 하나의 변수에 자료형이 서로 다른 데이터 값을 자유롭게 배정할 수 있음
  * 필요에 따라 또 다른 자료형의 데이터로 바꿀 수도 있음
  * 동적으로 선언한 변수는 프로그램의 실행 시점까지 자료형에 대한 검사를 하지 않음
 
* 예시 코드
```C#
class ClassA
{
  dynamic a = 10; //전역 변수로 사용할 수 있음

  public dynamic Add(int b) //반환자료형으로 사용할 수 있음
  {
    dynamic c; //선언과 동시에 값이 배정하지 않아도 됨
    c = a + b;
    return c;
  }
}

class ClassB
{
  public void PrintVar(dynamic d) //함수의 매개변수로 사용할 수 있음
  {
    Console.WriteLine(d);
    Console.WriteLine(d.GetType());
  }
}

class ClassC
{
  public string AddVars(int e, int f)
  {
    dynamic g = e + f; //정수값을 배정했기 때문에 g 역시 정수형으로 지정됨
    g = "James M."; //필요에 따라 전혀 다른 형태의 자료를 입력할 수 있음
    return g;
  }
}

class Program
{
  static void Main()
  {
    ClassB cb = new ClassB();

    //아래와 같이 하나의 함수에 서로 다른 형태의 인수를 전달하는 것이 가능함
    cb.PrintVar("C#"); //함수에 전달되는 값이 문자열(string) 타입임
    cb.PrintVar(123); //함수에 전달되는 값이 정수형(int32) 타입임

    ClsssC cc = new ClassC();
    Console.WriteLine(cc.AddVars(2, 3));
  }
}
```
* 동적 변수(dynamic) 특징
  * 지역 변수와 전역 변수에 모두 사용할 수 있음
  * 변수를 선언하는 시점에 반드시 값을 배정할 필요가 없음
  * 한 번 자료형이 결정된 이후에도 다른 형태의 자료를 입력할 수 있음
  * 함수의 반환값이나 매개변수에 사용할 수 있음
  * null 값을 가질 수 있음

* 동적 변수를 익명 타입에 사용한 예시 코드
```C#
static void Main()
{
  //익명 타입 선언
  dynamic a = new { Name = "James", Age = 35, EyeSight = 0.8 };

  //익명 타입 호출
  Console.WriteLine("이름 = {0}", a.Name);
  Console.WriteLine("나이 = {0}", a.Age);
  Console.WriteLine("언어 = {0}", a.EyeSight);

  Console.WriteLine();

  Console.Write("이름을 입력하세요: ");
  string x = Console.ReadLine();

  Console.Write("나이를 입력하세요: ");
  int y = int.Parse(Console.ReadLine());

  Console.Write("시력을 입력하세요: ");
  double z = double.Parse(Console.ReadLine());

  //익명 타입 선언
  dynamic b = new { Name = x, Age = y, EyeSight = z };

  //익명 타입 호출
  Console.WriteLine("이름 = {0}", b.Name);
  Console.WriteLine("나이 = {0}", b.Age);
  Console.WriteLine("언어 = {0}", b.EyeSight);

  Console.WriteLine();

  //각각의 자료형 확인
  Console.WriteLine(b.GetType());
  Console.WriteLine(b.Name.GetType());
  Console.WriteLine(b.Age.GetType());
  Console.WriteLine(b.EyeSight.GetType());
}
```

* 동적 변수(dynamic 타입) 많이 사용하는 경우 문제점
  * 프로그램의 실행 속도가 느려지고 리소스를 많이 차지함
  * 변수의 자료형이 프로그램 실행 시점에 결정됨 -> 더 많이 예외상황과 오류 가능성에 노출된다는 뜻
</div>
</details>

___

<details>
<summary>14. 서식 문자열</summary>
<div markdown="1">

</div>
</details>
