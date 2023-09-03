# 접근 제한자(public vs private), 캡슐화와 정보 은닉

<details>
<summary>접근 제한자 public vs private</summary>
<div markdown="1">       

#### public과 private의 차이
* public : 외부에서 클래스 혹은 클레스 멤버로의 접근을 허용함
* private : 클래스 밖에서 접근하는 것을 허용하지 않음
* 접근 제한자를 지정하지 않는 경우 기본값은 'private'임
* 예시
```C#
class ClassA
{
  private int a;
  private void PrintOutA()
  {
    Console.WriteLine(a);
  }
}

class ClassB
{
  public int b;
  public void PrintOutB()
  {
    Console.WriteLine(b);
  }
}

class Program
{
  static void Main()
  {
    ClassA x = new ClassA(); //ClassA의 인스턴스 생성
    x.a = 123; //오류!, 외부에서 private으로 선언된 객체에 값을 배정하고 있음
    x.PrintOutA(); //오류!, 외부에서 private으로 선언된 함수를 호출하고 있다.

    ClassB y = new ClassB(); //ClassB의 인스턴스 생성
    y.b = 123; //외부지만 public으로 선언된 객체인 경우 값을 배정할 수 있다.
    y.PrintOutB(); //외부지만 public으로 선언된 함수는 호출할 수 있다.
  }
}
```
</div>
</details>

___

<details>
<summary>캡슐화와 정보 은닉</summary>
<div markdown="1">       

#### 캡슐화(encapsulation, 혹은 정보 은닉, information hiding)의 기능
* 클래스 안의 객체들을 **하나로 묶어주는 기능**
* **묶어진 객체를 보호**하는 기능을 수행함
* 이러한 캡슐화는 접근 제한자를 통해 구현하게 됨
* 예시코드
```C#
class BankAccount
{
  private double balance = 0;

  public void Deposit(double n)
  {
    balance += n;
  }

  public void Withdraw(double n)
  {
    balance -= n;
  }

  public double GetBalance()
  {
    return balance;
  }
}
```
* balance는 private으로 선언해주었기 때문에 외부에저 직접 접근하거나 수정할 수 없음
  * 유일한 방법은 같은 클래스 안에서 public으로 선언된 Deposit(), Withdraw() 함수를 통해서만 가능함
  * balance에 저장된 값의 확인 역시 GetBalance() 함수를 통해서만 가능함
* 이러한 경우 balance는 **캡슐화**되었다고 표현하고,
* balance의 정보는 외부로부터 **숨겨졌다**(정보은닉)라고 말하는 것

#### 캡슐화의 장점
* 자료의 접근 제한을 통한 **값의 보존**
* 새로운 기능을 추가했을 때 **코드 수정의 용이함**
* 캡슐화된 부분을 수정했을 때, **클래스 외부에 끼치는 영향의 최소화**

#### 캡슐화를 사용한 프로그램 만들기
```C#
class BankAccount
{
  private double balance = 0;

  public void Deposit(double n)
  {
    balance += n;
  }

  public void Withdraw(double n)
  {
    balance -= n;
  }

  public double GetBalance()
  {
    return balance;
  }
}

class Program
{
  static void Main()
  {
    BankAccount acc = new BankAccount(); //클래스의 인스턴스 생성
    double money;
    int choice;

    do
    {
      Console.WriteLine("1. Deposit Money");
      Console.WriteLine("2. Withdraw Money");
      Console.WriteLine("3. Check Your Balance");
      Console.Write("Choose what you want: ");
      choice = Convert.ToInt16(Console.ReadLine());

      switch(choice)
      {
        case 1:
          Console.Write("How much do you want to deposit: ");
          money = Convert.ToDouble(Console.ReadLine());

          //BankAccount 클래스 안의 Deposit() 함수를 통해 balance를 수정하고 있다.
          acc.Deposit(money);
          Console.WriteLine("You have {0}", acc.GetBalance() + " won now.");
          break;

        case 2:
          Console.Write("How much do you want to withdraw: ");
          money = Convert.ToDouble(Console.ReadLine());

          //BankAccount 클래스 안의 Withdraw() 함수를 통해 balance를 수정하고 있다.
          acc.Withdraw(money);
          Console.WriteLine("You have {0}", acc.GetBalance() + " won now.");
          break;

        case 3:
          //BankAccount 클래스 안의 GetBalance() 함수를 호출하고 있다.
          Console.WriteLine("You have {0}", acc.GetBalance()+ " won now.");
          break;

        default:
          Console.WriteLine("You made a wrong choice!");
          break;
      }
    } while(choice < 4);
  }
}
```
* 외부에서 은행 잔고(balance)에 직접 접근할 방법은 없음
* 우회적으로 Deposit(), Withdraw(), GetBalance() 함수를 통해서만 은행 잔고에 접근하거나 수정할 수 있음
  * 이렇게 함으로써 잔액 자체에 대한 **외부의 접근과 수정을 막을 수 있으며**,
  * **각각의 함수들이 정확하게 어떤 연산을 수행하는지 외부에서 볼 수 없도록** 만들 수 있음
  * 즉, 과정은 감추고 결과만 보여주는 것, 이것이 바로 **캡슐화**임
* 접근제한자 public과 private을 적절하게 사용하면 혹시 모를 데이터의 변형을 막을 수 있음음  
</div>
</details>
