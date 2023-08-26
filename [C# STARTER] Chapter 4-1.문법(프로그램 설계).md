# 함수(메소드), 함수 호출 방법, 순환함수와 함수 오버로딩

## 함수(메소드)
* **함수(function)** : 하나의 목적을 구현하기 위한 명령문들의 집합으로, C#에서는 **메소드(method)** 라는 이름으로 부르기도 함
  * C# 자체에 내장된 함수 이외에도 필요에 따라 직접 함수를 선언해서 사용할 수 있음
  * 함수를 사용하면 코드의 재사용, 모의 실행의 단순화 등 다양한 이점이 생김
> 반환자료형 함수명(자료형1 매개변수1, 자료형2, 매개변수2, ...)

> {

>   statement(s);

> } 
    
<details>
<summary>1. 함수 선언</summary>
<div markdown="1">       

```C#
double SquareRoot(double x)
{
  double result = x * x;
  return result;
}
```
```C#
void ConsolePrint(double x)
{
  Console.WriteLine(x);
}
```
* 함수를 정의할 때는 반환값의 자료형(반환자료형)과 함수의 이름을 먼저 적어주고, 괄호 뒤에 매개변수를 정의해주면 됨
  * 매개변수는 필요한 만큼 정의해주면 됨(필요 없는 경우, 생략 가능)
* 함수는 **호출된 뒤에 값을 반환하는 함수**와 **연산만 수행하는 함수**로 나뉨
  * 호출된 뒤 값을 반환하는 함수는 반드시 **return 명령문**을 가져야 함
  * 연산만 수행하는 함수의 경우 return 명령문을 가지지 않음, 대신 반환자료형에 **void**라고 적어주어야 함 
</div>
</details> 

<details>
<summary>2. 함수 호출</summary>
<div markdown="1">       

```C#
static void HelloWorld(int x) //HelloWorld 함수 선언
{
  Console.WriteLine($"Hello World! ...{x}");
}

static void Main()
{
  Console.Write("함수를 몇 번 호출할까요? ");
  int x = Convert.ToInt16(Console.ReadLine());

  while(x > 0)
  {
    HelloWorld(x); //HelloWorld 함수 호출
    x--;
  }
}
```
  * 함수를 호출하는 방법은 단지 해당 함수가 필요한 자리에서 함수의 이름과 필요한 매개변수 값을 제시하면 됨

```C#
static void Main()
{
  Console.Write("제곱근을 계산하고자 하는 수를 입력하세요: ");
  double y = Convert.ToDouble(Console.ReadLine());

  Console.WriteLine("{0}의 제곱은 {1}dlqslek.", y, SquareRoot(y)); //함수 호출
}

static double SquareRoot(double x) //함수 선언
{
  double result = x * x;
  return result;
}
```
* 앞 코드와 달리 SquareRoot() 함수가 Main() 함수보다 나중에 선언되고 있음
  * 즉, 자신을 사용하게 될 자리보다 앞에서 함수를 선언하든 뒤에서 선언하든 상관없다는 뜻!
* 또한, 선언된 매개변수의 자료형이 일치하는지만 중요할 뿐, 매개변수의 이름까지 똑같을 필요는 없음

```C#
static double Addition(double x, double y)
{
  return x + y;
}

static double Subtraction(double x, double y)
{
  return x - y;
}
```
* 하나의 함수를 선언할 때 매개변수를 몇 개까지 쓸 수 있는지에 대한 제한은 없음
* 단, 여러 개의 매개변수를 선언할 때에는 자료형을 함께 명시해주어야 하며, 각각의 매개변수는 콤마(,)로 구별함

* 계산기 프로그램 함수 코드(예시)
```C#
static double Addition(double x, double y)
{
  return x + y;
}

static double Subtraction(double x, double y)
{
  return x - y;
}

static double Multiplication(double x, double y)
{
  return x * y;
}

static double Division(double x, double y)
{
  return x / y;
}

static void Main()
{
  do
  {
    Console.WirteLine("어떤 계산을 원하십니까?");
    Console.WriteLine("1. 덧셈");
    Console.WriteLine("2. 뺄셈");
    Console.WriteLine("3. 곱셈");
    Console.WriteLine("4. 나눗셈");
    Console.WriteLine("5. 나가기");
    int choice = Convert.ToInt16(Console.ReadLine());

    if(choice > 4)
    { break; }

    else
    {
      Console.Write("\nx = ");
      double x = Convert.ToDouble(Console.ReadLine());

      Console.Write("y = ");
      double y = Convert.ToDouble(Console.ReadLine());

      switch(choice)
      {
        case 1:
          Console.WriteLine("\nx + y = {0}\n", Addition(x, y));
          break;

        case 2:
          Console.WriteLine("\nx - y = {0}\n", Subtraction(x, y));
          break;

        case 3:
          Console.WriteLine("\nx * y = {0}\n", Multiplication(x, y));
          break;

        case 4:
          Console.WriteLine("\nx / y = {0}\n", Division(x, y));
          break;
      }
    }
  } while(true);
}
```
* 매개변수 vs 인수
  * 매개변수 : 파라미터라고도 불리며, 함수를 선언할 때 외부에서 입력값을 받기 위해 정의된 변수(함수를 위한 변수)를 말함
    * 오직 함수를 위해 존재하므로 함수의 역할이 끝나면 매개변수도 함께 사라짐 
  * 인수(argument) : 함수에 실제로 전달되는 데이터값을 부르는 이름 
</div>
</details>

<details>
<summary>3. 인수 전달 방법 1</summary>
<div markdown="1">       

* 함수를 호출하면서 함께 전달하는 게 일반적인 방법
```C#
static void Addition(int x, int y)
{
  Console.WriteLine(x, y);
}

static void Main()
{
  int x = 3;
  int y = 5;

  Addition(x, y); //일반적인 인수 전달 방법
}
```
</div>
</details>

<details>
<summary>4. 인수 전달 방법 2</summary>
<div markdown="1">       

* 함수를 정의하면서 매개변수를 선언할 때 해당 매개변수의 기본값을 배정할 수 있음
  * 장점 1 : 사용자가 입력값을 제공하지 않은 경우, 유연하게 대처할 수 있음
  * 장점 2 : 사용자에게 좀 더 넓은 선택의 폭을 제공할 수 있음
```C#
//함수를 선언하면서 매개변수의 기본값을 배정하고 있다.
static double PoweringNumber(double x = 3.0, int y = 3)
{
  double result = 1.0;

  for(int i = 0; i < y; i++)
  {
    result *= x;
  }

  return result;
}

static void Main()
{
  //매개변수 없이 함수 호출 - OK(이미 함수를 호출할 때 기본값을 배정해두었기 때문)
  Console.WriteLine(PoweringNumber());
  COnsole.WriteLine();

  //매개변수 중 앞의 값만 제공해서 함수 호출 - OK
  Console.WriteLine(PoweringNumber(5));
  Console.WriteLine();

  //매개변수의 값 모두를 제공하면서 함수 호출 - OK
  Console.WriteLine(PoweringNumber(5, 5));
  Console.WriteLine();

  Console.Write("아무 수나 입력하세요: ");
  double baseNum = Convert.ToDouble(Console.ReadLine());

  Console.Write("입력한 수를 몇 번 곱할까요? ");
  int powerNum = Convert.ToInt16(Console.ReadLine());

  //(일반적인 방법) 사용자 입력을 매개변수로 사용 - OK
  Console.WriteLine(PoweringNumber(basaeNum, powerNum));
}
```
* 앞의 인수를 빼고 뒤에 있는 인수만 제공하는 것은 허용되지 않음
> ex. Console.WriteLine(PoweringNum(, 5)); 등 오류 발생
</div>
</details>

<details>
<summary>5. 인수 전달 방법 3</summary>
<div markdown="1">       

* 함수에 넘겨주는 인수값은 함수를 정의하면서 선언한 매개변수의 순서를 그대로 따라야 함
* But, 함수 안에 정의된 매개변수의 이름을 알고 있다면, 이 순서를 무시하고 인수를 넘길 수 있음
```C#
static double Area(double height, double width)
{
  return height * width;
}

static void Main()
{
  Console.Write("가로의 길이를 입력하세요: ");
  double w = Convert.ToDouble(Console.ReadLine());

  Console.Write("세로의 길이를 입력하세요: ");
  double h = Convert.ToDouble(Console.ReadLine());

  //다음 3개의 명령문은 같은 결과를 출력할 것이다.

  //Area(w, h)는 오류의 원인이 됨
  Console.WriteLine(Area(h, w));

  //각각의 인수가 어떤 매개변수로 전달되는지 정하고 있다. - OK
  Console.WriteLine(Area(width: w, height: h));
  Console.WriteLine(Area(height: h, width: w));
}
```
* <매개변수 이름: 인수 값>형식으로 어느 인수를 어느 매개변수에 전달할 것인지 지정해준다면 인수의 전달 순서를 지키지 않아도 됨
> Console.WriteLine(Area(width: w, height: h)); = Console.WriteLine(Area(height: h, width: w));
</div>
</details>

## 함수 호출 방법

## 순환함수와 함수 오버로딩
