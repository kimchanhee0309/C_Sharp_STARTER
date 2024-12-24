# 클래스, 함수, 프로퍼티, 생성자 비교, 접근 제한자 readonly

<details>
<summary>클래스, 함수, 프로퍼티, 생성자 비교</summary>
<div markdown="1">       

### 예시 코드를 통해 알아보는 클래스, 함수, 프로퍼티, 생성자의 차이
```C#
class ClassName //클래스 선언
{
  //클래스 내 변수 선언
  private int result = 10;

  //반환값이 없는 함수 선언
  public void setResult(int result)
  { this.result = result; }

  //반환값이 있는 함수 선언
  public int getResult()
  { return result; }

  //프로퍼티 선언:
  //클래스의 멤버 변수(result)와 같은 이름을 가지며 괄호()를 가지지 않는다.
  public int Result
  {
    set { result = value; } //setter
    get { return result; } //getter
  }

  private int result2; //클래스 내 변수 선언

  //자동 구현 프로퍼티 선언:
  //클래스의 멤버 변수(result2)와 같은 이름을 가지며 괄호()를 가지지 않는다.
  public int Result2
  { set; get; }

  //생성자 선언:
  //반환자료형을 가지지 않으며, void 키워드를 사용하지 않는다.
  public ClassName()
  { Console.WriteLine("클래스가 만들어졌습니다.\n"); }
}

class Program
{
  static void Main()
  {
    //클래스 인스턴스 생성: 이때 생성자가 함께 호출된다.
    ClassName c = new Classname();

    Console.Write("정수를 입력하세요: ");
    int x = int.Parse(Console.ReadLine());

    //ClassName 클래스의 setResult(), getResult() 함수 사용 예시
    c.setResult(x);
    Console.WriteLine("첫 번째 입력값은 = {0}", c.getResult());

    Console.Write("또 다른 정수를 입력하세요: ");
    int y = int.Parse(Console.ReadLine());

    //프로퍼티와 자동 구현 프로퍼티의 사용법은 같다.

    //프로퍼티의 사용
    c.Result = y;
    Console.WriteLine("두 번째 입력값은 = {0}", c.Result);

    //자동 구현 프로퍼티의 사용
    c.Result2 = 999;
    Console.WriteLine("자동구현 프로퍼티에 의한 입력값은 = {0}", c.Result2);
  }
}
```
</div>
</details>

___

<details>
<summary>접근 제한자 readonly</summary>
<div markdown="1">       

### readonly 접근 제한자란?
* 클래스의 멤버 변수의 값이 최초 선언된 이후에 수정되는 것을 막아줌
  
### 상수와의 차이점
* 상수는 선언되는 시점에 반드시 값이 주어져야 하지만 readonly는 선언할 때 값이 주어지지 않아도 된다.
  >const string name;
  >
  >readonly string name;
* 상수는 계산식의 값을 배정받을 수 없지만, readonly는 계산식의 값을 배정받을 수 있다.
  >const int x = 2 * 5;
  >
  >readonly int x = 2 * 5;
* 상수의 경우 한 번 배정된 값은 바꿀 수 없지만, readonly로 선언된 변수는 **생성자**를 통하는 경우 필요할 때마다 그 값을 바꿀 수 있다.

### 예시 코드를 통해 알아보는 접근 제한자 readonly
```C#
class Users
{
  private readonly string userID;
  private readonly string userPW;

  public Users(string id, string pw) //생성자 선언
  {
    //생성자를 통해 값을 바꾸도록 하고 있다.
    this.userID = id;
    this.userPW = pw;
  }

  public void Print() //출력 함수 선언
  {
    Console.WriteLine("Your ID is {0}", this.userID);
    Console.WriteLine("Your PW is {0}", this.userPW);
  }
}

class Program
{
  static void Main()
  {
    string uID;
    string uPW;

    do
    {
      Console.Write("아이디를 입력하세요: ");
      uID = Console.ReadLine();

      Console.Write("비밀번호를 입력하세요: ");
      uPW = Console.ReadLine();

      //uID와 uPW를 위한 값이 모두 입력되었는지 확인한다.
      if((uID.Length == 0) || (uPW.Length == 0))
      {
        Console.WriteLine("올바른 입력값이 아닙니다.");
        break; //do-while 문을 종료한다.
      }

      //Users 클래스의 인스턴스를 생성한다.
      Users u = new Users(uID, uPW);
      u.Print(); //출력 함수 실행: 결과는 사용자의 입력값

    } while ((uID.Length != 0) && (uPW.Length != 0));
  }
}
```
* 만약, 이 부분을 const로 수정해서 선언한다면?
  >private readonly string userID; -> private const string userID = "James";
  > 
  >private readonly string userPW; -> private const string userPW = "12345";
* 오류가 발생한다.
  * why? **상수(const)** 로 선언한 경우에는 프로그램이 실행되는 동안 그 값을 바꿀 수 없기 때문임
* const와 readonly가 가지는 결정적 차이점
  * const가 `컴파일 타임 상수` 즉, 코드를 컴파일할 때 값을 배정하는 상수라면,
  * readonly는 `런타임 상수` 즉, 프로그램이 실행되는 순간 값을 배정하는 상수임
* So, 프로그램이 실행되는 시점에 한 번만 사용자를 확인하고, 로그인을 마친 사용자의 상태는 프로그램이 종료될 때까지 그대로 유지되어야 하는 경우에 `readonly`를 사용할 수 있음
  * 이를 활용하면 로그인 시점에서 한 번 입력한 정보는 프로그램이 종료될 때까지 그 값이 변하지 않을 것임!

</div>
</details>
