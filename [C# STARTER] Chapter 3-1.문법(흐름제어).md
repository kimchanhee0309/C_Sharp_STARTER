# 조건문과 비교 연산자

## 조건문
**if문**
* 주어진 조건이 참인 경우에만 주어진 코드 블럭을 실행함
* if문의 시작과 끝은 반드시 중괄호 {}로 감싸주어야 함
* 조건이 거짓인 경우, if문을 빠져나오는 대신 else문이 작동함(else문은 별도의 조건식을 가지지 않음)
* else if문은 if문의 조건이 거짓인 경우 바로 else문으로 넘어가지 않고, 또 다른 조건에 부합하는지 확인하기 위해 사용(별도의 조건식 가짐)
* if -> else if -> else의 순서는 반드시 지켜야 함
* ※ 문자열에만 적용할 수 있는 3가지 함수
   * ToUpper() : 문자열의 모든 글자를 대문자로 변환한다.
   * ToLower() : 문자열의 모든 글자를 소문자로 변환한다.
   * ToTitleCase() : 각 단어의 첫 글자를 대문자로 변환하고 나머지 글자는 모두 소문자로 변환한다.
```C#
static void Main(string[] args)
{
  Console.Write("What is your grade on C# test? ");
  char grade = Convert.ToChar(Console.ReadLine().ToUpper());

  if(grade == 'A')
  {
    Console.WriteLine("Excellent!");
  }

  else if(grade == 'B')
  {
    Console.WriteLine("Good job");
  }

  else if(grade == 'C')
  {
    Console.WriteLine("You're passed.");
  }

  else if(grade == 'D')
  {
    Console.WriteLine("You should have studied harder.");
  }

  else if(grade == 'F')
  {
    Console.WriteLine("You're failed.");
  }

  else
  {
    Console.WriteLine("You made a wrong input.");
  }
}
```

**switch문**
* switch문은 if문에 비해 가독성이 좋기 때문에 자주 사용함
* case에 제시된 조건 중 하나라도 만족하면 break문을 실행한 뒤 전체 코드 블럭에서 빠져나옴
* switch문
   * 반드시 case문이 있어야 함
   * default는 필수가 아님. 이는 case문에 제시된 조건 중 어떤 것에도 만족하지 않을 때 실행하는 코드로, if문에서의 else와 같은 기능을 수행 
* case문
   * 조건을 제시한 후에 콜론(:)으로 끝나야 함
   * 반드시 break 명령어를 가져야 switch문이 종료됨
* 쓰임이 다양함(예시 코드 2개)
```C#
static void Main(string[] args)
{
  Console.Write("What is your grade on C# test? ");
  char grade = Convert.ToChar(Console.ReadLine().ToUpper());

  switch(grade)
  {
    case 'A':
      Console.WriteLine("Excellent!");
      break;

    case 'B':
      Console.WriteLine("Good job!");
      break;

    case 'C':
      Console.WriteLine("You're passed.");
      break;

    case 'D':
      Console.WriteLine("You should have studied harder.");
      break;

    case 'F':
      Console.WriteLine("You're failed");
      break;

    default:
      Console.WriteLine("You made a wrong input.");
      break;
  }
}
```
```C#
static void Main(string[] args)
{
  Console.Write("1~9 범위의 수를 입력하시오: ");
  int x = int.Parse(Console.ReadLine());

  switch(x)
  {
    case 1:
    case 2:
    case 3:
      Console.WriteLine($"{x}은(는) 낮은 범위의 수 입니다.");
      break;

    case 4:
    case 5:
    case 6:
      Console.WriteLine($"{x}은(는) 중간 범위의 숫 입니다.");
      break;

    case 7:
    case 8:
    case 9:
      Console.WriteLine($"{x}은(는) 높은 범위의 숫 입니다.");
      break;

    default:
      Console.WriteLine($"{x}은(는) 잘못된 입력입니다.");
      break;
  }
}
```
* 다음과 같은 구성이면, 1,2,3을 똑같은 조건으로, 4,5,6을 똑같은 조건으로, 7,8,9를 똑같은 조건으로 간주함

___
## 비교 연산자
