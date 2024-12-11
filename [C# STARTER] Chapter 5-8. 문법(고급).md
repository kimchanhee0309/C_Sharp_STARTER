# 예외 처리

<details>
<summary>15. 예외 처리</summary>
<div markdown="1">

### try-catch 문
* 예시 코드
```C#
try
{
  int[] arr = new int[3];

  for (int i = 0; i < arr.Length; i++)
  {
    Console.Write("정수를 입력하세요: ");
    arr[i] = Convert.ToInt32(Console.ReadLine());
  }

  for (int i = 0; i < arr.Length; i++)
  {
    Console.WriteLine("입력한 정수는 {0}입니다.", arr[i]);
  }
}

catch (Exception e)
{
  Console.WriteLine("오류 발생! 정수가 아닙니다.");
}
```
* Exception은 모든 종류의 예외상황에 대한 정보를 가지고 있음
* 어떤 예외상황이 발생했는지 알고 싶을 땐 다음과 같은 명령문을 추가하면 됨
> Console.WriteLine(e.message);

* 하나의 try 문은 필요한 만큼의 catch 문을 가질 수 있음
  * 각각의 예외상황마다 다르게 대치하고 싶은 경우, 여러 개의 catch 문을 만들어 주면 됨. 이를 **다중 catch문** 이라고 함
* 예시 코드
```C#
try
{
  Console.Write("정수를 입력하세요: ") ;
  int x = Convert.ToInt32(Console.ReadLine());

  Console.WriteLine(x);
}

catch (OverflowException ovf)
{
  Console.WriteLine(ovf.Message);
}

catch (Exception ex)
{
  Console.WriteLine(ex.Message);
}
```
* 일반적으로 사용되는 예외처리기

예외처리기 | 의미 
----------------- | ------------------ 
FileNotFoundException | 지정한 파일을 찾을 수 없음
DirectoryNotFoundException | 디렉토리 경로가 올바르지 않음
DriveNotFoundException | 드라이브를 사용할 수 없거나 찾을 수 없음
FormatException | 지정한 값을 문자열로 형변환할 수 있음
IndexOutOfRangeException | 배열에서 지정한 인덱스의 범위를 벗어남
TimeoutException | 작업에 할당된 시간이 만료됨
OutOfMemoryException | 시스템 메모리를 할당할 수 없음
OverflowException | 산술이나 형변환의 결과가 범위를 벗어남
ArgumentException | 함수에 전달되는 인수값이 올바르지 않음
ArgumentOutOfRangeException | 함수에 전달되는 인수값이 범위를 벗어남
DivideByZeroException | '0'을 분모로 하여 나눗셈 연산을 함
NotSupportedException | 지원하지 않는 연산을 실행함
NullReferenceException | 값을 배정받지 않은 변수를 참조하여 연산함

### finally 문
* 특징
  * catch 문 뒤에 선택적으로 사용할 수 있음
  * 예외상황의 발생과 상관없이 무조건 실행됨
  * 반드시 존재해야 하는 건 아니지만, 예외 상황이 발생했을 때 낭비되는 리소스를 반환하고자 할 때 효율적임
  * 예시 코드
  ```C#
  for (int i = 0; i < 3; i++)
  {
    try
    {
      Console.Write("분자를 입력하세요: ");
      int x = Convert.ToInt32(Console.ReadLine());

      Console.Write("분모를 입력하세요: ");
      int y = Convert.ToInt32(Console.ReadLine());

      Console.WriteLine(x/y);
    }

    catch (Exception e)
    {
      Console.WriteLine(e.Message);
    }
  }
  ```
  * try 문은 반드시 하나 이상의 catch문 혹은 finally문을 가져야 함. 어느 것도 가지지 않는다면 오류의 원인이 됨

### throw 문
* try-catch 문과 달리 개발자가 원하는 자리에서 원하는 조건의 예외처리기를 호출할 때 쓰이는 문
* 예외처리기를 수동적으로 호출하는 방법임
* 예시 코드
```C#
class Program
{
  static string password = "#123";

  static void Main()
  {
    Console.Write("비밀번호를 입력하세요: ");
    string pw = Console.ReadLine();

    if (password != pw)
    {
      //예외처리기를 호출하고 프로그램을 종료한다.
      throw new Exception("비밀번호가 잘못되었습니다.");
    }
    else
    {
      Console.WriteLine("로그인 되었습니다.");
    }
  }
}
```

```C#
class Program
{
  static string password = "#123";

  static void Main()
  {
    string pw;

    try
    {
      for (int counter = 3; counter > 0; )
      {
        Console.Write("비밀번호를 입력하세요: ");
        pw = Console.ReadLine();

        if (password != pw)
        {
          Console.WriteLine("비밀번호가 잘못되었습니다.");
          counter--;

          Console.WriteLine();

          if (counter == 0)
          {
            //예외처리기를 호출하고 프로그램을 종료한다.
            throw new Exception("비밀번호를 3회 잘못 입력했습니다.");
          }
        }

        else
        {
          //예외처리기를 호출하고 프로그램을 종료한다.
          throw new Exception("로그인 되었습니다.");
        }
      }
    }
    catch(Exception e)
    {
      Console.WriteLine(e.Message);
    }
  }
}
```
* try-catch 문 없이 throw 문만 사용한 경우에는 finally 문을 사용할 수 없음

</div>
</details>
