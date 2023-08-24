# 반복문과 논리 연산자

## 반복문

* 주어진 조건이 '참'일 때 한 번만 실행하는 `조건문`과 달리, `반복문`을 사용하면 조건이 '참'인 동안 제시한 명령문을 **반복해서 실행**함
  
<details>
<summary>1. while문</summary>
<div markdown="1">       

```C#
//'x'가 10보다 작은 동안 'x' 값을 계속 출력하는 코드
static void Main(string[] args)
{
  int x = 1;

  while(x < 10)
  {
    Console.WriteLine(x);
    x++;
  }
}
```
```C#
static void Main(string[] args)
{
  int y = 0;

  //조건식 안에 증가연산자를 사용하고 있다.
  //먼저 값을 증가시킨 뒤에 비교하고 있다.
  while(++y < 10)
  {
    Console.WriteLine(y);
  }

  Console.WriteLine();

  int z = 0;

  //비교를 먼저 한 뒤에 값을 증가시키고 있다.
  while(z++ < 10)
  {
    Console.WriteLine(z);
  }
}
```

* while문 사용 시 주의해야 할 점
  * 반복이 끝나는 조건을 명확하게 제시해야 함
* while문 안에서는 증감연산자 뿐만 아니라 일반적인 산술연산자도 사용할 수 있음(조건식 안에서도 사용 가능)
* 중첩 while문 : while문을 중첩해서 사용
  * 구구단 예시 
```C#
static void Main(string[] args)
{
  int x = 0;
  int y = 0;

  while(x < 9)
  {
    x++;

    while(y < 9)
    {
      y++;
      Console.WriteLine("{0} 곱하기 {1} = {2}", x, y, x*y);
    }

    y = 0; //x단 끝난 후 y 초기화
  }
}
```
</div>
</details>

<details>
<summary>2. do-while문</summary>
<div markdown="1">       

* while문의 경우 : 주어진 조건이 거짓이라면 한 번도 실행되지 않을 수 있는 반면,
* do-while문의 경우 : 주어진 조건의 참/거짓 여부와 상관없이 최소한 한 번은 실행된다는 점에서 차이를 보임
  * 조건식 붙는 자리가 코드 블럭의 '뒤'라는 점과 조건식 뒤에 세미콜론을 붙인다는 점에서도 차이를 보임 
```C#
static void Main(string[] args)
{
  int x = 1;

  do
  {
    Console.WriteLine(x);
    x++;
  } while(x > 10); // 'x'가 10보다 큰 값인 동안 반복, 이 코드에서는 거짓이기 때문에 한 번만 출력함
}
```
```C#
static void Main(string[] args)
{
  int y = 1;

  do
  {
    Console.WriteLine(y);
    y++;
  } while ( y < 10); // 'y'가 10보다 작은 동안 반복 실행, 1~9까지 아홉 번의 출력이 이루어짐
}
```
</div>
</details>

<details>
<summary>3. for문</summary>
<div markdown="1">       

* 반복 횟수를 관리하기 위한 **카운터(counter)** 를 가짐
  * 카운터로 사용되는 변수는 반드시 **정수형(integer)** 이어야 함
  * for문에서는 같은 이름을 가진 카운터 변수를 다시 선언할 수 있음(for문 안에서만 일회성으로 사용됨)
```C#
static void Main(string[] args)
{
  //다음 조건식에서 'x'를 카운터라고 부른다.
  for(int x = 9; x > 0; x--)
  {
    Console.WriteLine(x);
  }

  COnsole.WriteLine(); //공백 줄 삽입

  //다음 조건식에서 'x'를 카운터라고 부른다.
  for(int x = 1; x < 10; x++)
  {
    Console.WriteLine(x);
  }
}
```
  * for문 안에서 선언한 변수는 for문 밖에서 사용할 수 없지만, for문 밖에서 선언된 일반적인 변수를 for문의 카운터로 사용하는 것은 가능함
    * 밖에서 선언된 변수를 사용하는 경우, for문에서 따로 선언하지 않아야 하며, 세미콜론만 적어주면 됨
```C#
static void Main(string[] args)
{
  int num = 1;

  //카운터를 선언하는 대신 그냥 세미콜론만 적어 준다.
  for( ; num < 10; num++)
  {
    Console.WriteLine(num);
  }

  //for문을 벗어난 뒤에도 변수의 값이 유지됨
  Console.WriteLine("\n변수 num의 현재값은 = {0}", num);
}
```
  * 카운터의 연산식 역시 원한다면 for문의 코드블럭 안에 기술할 수 있음(세미콜론은 반드시 유지!)
```C#
static void Main(string[] args)
{
  //카운터 연산식 대신 세미콜론만 적어주고 있다.
  for(int num = 1; num < 10 ; )
  {
    Console.WriteLine(num);
    num++; //카운터 변수의 증가를 조건식이 아닌 for문 안에서 하고 있음
  }
}
```
  * 같은 기능을 수행하는 2개의 for문 예시
```C#
static void Main(strin[] args)
{
  for(int num = 1; num < 10; num++)
  {
    Console.WriteLine(num);
  }

  Console.WriteLine();

  for(int num = 1; num < 10 ; )
  {
    Console.WriteLine(num);
    num++;
  }
}
```
  * for문의 카운터 연산식을 위해 산술연산자를 사용할 수도 있음
```C#
static void Main(string[] args)
{
  for(int x = 1; x <= 10; x += 2)
  {
    Console.WriteLine("The number is now {0}", x);
  }

  Console.WriteLine();

  for(int x = 10; x >= 1; x -= 2)
  {
    Console.WriteLine("The number is now {0}", x);
  }
}
```
</div>
</details>

<details>
<summary>4. foreach문</summary>
<div markdown="1">       

* `배열` 또는 `컬렉션 구조`에 특화된 반복문
* 배열의 각 인덱스를 차례대로 접근하여 데이터값을 수정할 수 있도록 해줌
</div>
</details>

<details>
<summary>5. break 명령어</summary>
<div markdown="1">       
  
 * break문을 위한 조건식을 따로 제시하고, 이 조건의 참/거짓 여부에 따라 반복문의 실행을 중단하도록 만드는 것
 * break문을 적절하게 추가하지 않는다면 **무한 루프**에 빠지게 됨
 * 무한 루프에 빠진 예시와 탈출하는 예시
```C#
//무한 루프 빠진 예시
static void Main(string[] args)
{
  int x = 0;

  Console.Write("Give me a number smaller than 10: ");
  x = Convert.ToInt32(Console.ReadLine());

  while( x <= 10) 
  {
    Console.WriteLine(x);
    x--;
  } 
}
//정수형은 음수도 포함하기 때문에 while문이 끝나는 조건을 제시하지 못함(무한 루프)
```
```C#
static void Main(string[])
{
  int x = 0;

  Console.Write("Give me a number smaller than 10: ");
  x = Convert.ToInt32(Console.ReadLine());

  while( x <= 10) 
  {
    if( x < 0 )
    {
      break;
    }

    Console.WriteLine(x);
    x--;
  } 
}
```
  * for문에서도 작동함
```C#
static void Main(string[])
{
  int x = 0;

  Console.Write("Give me a number smaller than 10: ");
  x = Convert.ToInt32(Console.ReadLine());

  for( ; x <= 10 ; x--) 
  {
    if( x < 0 )
    {
      break;
    }

    Console.WriteLine(x);
    x--;
  } 
}
```
  * 주의할 점
    *  자신이 속한 반복문에서만 빠져나올 뿐, 그보다 상위 개념의 반복문에서 빠져 나오는 것은 아니라는 사실!
```C#
static void Main(string[] args)
{
  Console.WriteLine("10보다 작거나 같은 수를 입력하세요: ");
  int x = Convert.ToInt32(Console.ReadLine());

  while(x <= 10) //상위 while문
  {
    while(x >= 4) //하위 while문
    {
      if(x == 3)
      {
        break; //하위 while문의 종료
      }

      Console.WriteLine($"Hello! {x}");
      x--;
    }

    Console.WriteLine($"See you later! {X}");
    x--;

    if(x == 0)
    {
      break; //상위 while문의 종료
    }
  }
}
```

</div>
</details>

<details>
<summary>6. continue 명령어</summary>
<div markdown="1">       

* break와 달리 반복문을 종료시키지 않고, 주어진 조건에 만족하는 연산만 건너 뛰게 만드는 역할
```C#
static void Main(string[] args)
{
  for(int y = 1; y <=10; y++)
  {
    if(y % 2 == 0)
    {
      continue; //2로 나눈 나머지가 0인 경우(짝수인 경우) 반복문을 건너 뜀, 즉 홀수만 출력
    }
  }
}
```
  * 주의점 : break, continue 모두 조건이 충족되는 순간 자신이 속한 반복문으로부터 빠져나온다는 점(무한 루프에 빠질 수 있음)
```C#
static void Main(string[] args)
{
  int a = 1;

  while(a <= 20)
  {
    if(a <= 10)
    {
      Continue;
      a++; //무한 루프의 원인
    }
    Console.WriteLine($"현재 'a'값은 = {0}");
    a++;
  }
}
```
```C#
//무한 루프 해결법
static void Main(string[] args)
{
  int a = 1;

  while(a <= 20)
  {
    if(a <= 10)
    {
      a++; //일단 증가 연산을 수행한 후에 continue를 실행한다.
      Continue;
    }
    Console.WriteLine($"현재 'a'값은 = {0}");
    a++;
  }
}
```
</div>
</details>

___

## 논리 연산자
<details>
<summary>1. 논리 연산자의 종류</summary>
<div markdown="1">       


|**연산자**|**이름**|**형태**|**참의 조건**|
|:---:|:---:|:---:|:---:|
|&&|AND 연산자|x && y|좌우가 **모두 참**인 경우에만 결과값이 참|
|ll|OR 연산자|x ll y|좌우 중 **하나만 참**이어도 결과값은 참|
|!|NOT 연산자|!x|주어진 값이 참이면 결과값은 거짓, 주어진 값이 거짓이면 결과값은 참|

* 예시 코드
```C#
static void Main(string[] args)
{
  int age = 0;
  int haveID = 0;
  int haveMembership = 0;

  Console.Write("당신의 나이는 18세 이상입니까? (Yes = 1, No = 0) ");
  age = Convert.ToInt16(Console.ReadLine());

  Console.Write("신분증을 가지고 있습니까? (Yes = 1, No = 0) ");
  haveID = Convert.ToInt16(Console.ReadLine());

  Console.Write("멤버십을 가지고 있습니까? (Yes = 1, No = 0) ");
  haveMembership = Convert.ToInt16(Console.ReadLine());

  if(age == 1 && ( haveID == 1 || haveMembership == 1))
  {
    Console.WriteLine("입장이 허가되었습니다.");
  }

  else
  {
    Console.WriteLine("입장이 거부되었습니다.");
  }
}
```
 * 몇 개의 논리 연산자를 사용할 수 있는지에 대한 제한은 없음
 * 논리 연산자들 사이에 우선순위는 존재하지 않음
   * 즉, 왼쪽에서 오른쪽으로 쓰여진 순서대로 연산지 이루어짐
   * 여러 논리 연산자를 함께 사용할 때에는 반드시 괄호를 사용하여 알아보기 쉽게 작성하기
     
|**연산자**|**경우의 수**|**결과값**|
|:--------:|:----------:|:---------:|
|AND       |true && true|true       |
|  ''      |true && false|false     |
|  ''      |false && false|false    |
|OR        |ture \|\| true  |true   |
|''|true \|\| false | true |
|''|false \|\| true | true |
|''|false \|\| false | false |
|NOT|!true|false|
|''|!false|true|
</div>
</details>

<details>
<summary>2. 계산기 프로그램</summary>
<div markdown="1">       

```C#
static void Main(string[] args)
{
  do
  {
    Console.WriteLine("Which calculation do you want to do?");
    Console.WirteLine("1. addition");
    Console.WirteLine("2. subtraction");
    Console.WirteLine("3. multiplication");
    Console.WirteLine("4. division");
    Console.WirteLine("5. exit");
    int choice = Convert.ToInt16(Console.ReadLine());

    if(choice > 4 || choice < 1)
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
          double addition = x + y;
          Console.WriteLine("\nx + y = {0}\n", addition);
          break;

        case 2:
          double subtraction = x - y;
          Console.WriteLine("\nx - y = {0}\n", subtraction);
          break;

        case 3:
          double multiplication = x * y;
          Console.WriteLine("\nx * y = {0}\n", multiplication);
          break;

        case 1:
          double division = x / y;
          Console.WriteLine("\nx / y = {0}\n", division);
          break;
      }
    }
  } while(true);
}
```
 * 조건식 자체를 '참'이라고 설정했기 때문에, 무한루프를 발생시킴
 * 무한루프를 멈추기 위해  `if(choice > 4 || choice < 1) { break; }` 명령문을 사용함
</div>
</details>
