# 인덱서, 열거형 클래스

<details>
<summary>1. 인덱서</summary>
<div markdown="1">       

### 인덱서(indexer)란?
* 배열과 프로퍼티의 특징을 모두 가지는 객체
* **배열을 캡슐화**하여 외부의 접근을 제한적으로 허용하는 특별한 도구임
* 클래스를 배열처럼 사용할 수 있게 해

### 인덱서와 프로퍼티(property)를 구별하는 3가지 측면
* 인덱서를 정의할 때는 변수명을 사용하지 않고 **'this' 키워드를 사용**함
* 프로퍼티가 매개변수를 사용하지 않는 것과 달리, 인덱서는 **배열을 위한 매개변수를 사용**함
* 인덱서는 **자동 구현 프로퍼티**를 지원하지 않음

### 예시 코드
```C#
class IdxDemo
{
  private int[] num = new int[5];

  //다음 this가 가리키는 것은 private 배열 변수 num이다.
  public int this[int x]
  {
    set { num[x] = value; }
    get { return num[x]; }
  }
}

class Program
{
  static void Main()
  {
    /* 다음 test를 배열로 선언하지 않았는데 배열처럼 사용할 수 있는 것은
       클래스 안에 인덱서(배열 프로퍼티)가 존재하기 때문임. */
    IdxDemo test = new IdxDemo();

    for(int x = 0; x < 5; x++)
    {
      //test 클래스를 배열처럼 사용하고 있음
      test[x] = x;
      Console.WriteLine(test[x]);
    }
  }
}
```
* 'IdxDemo' 클래스의 인스턴스인 'test'를 선언한 뒤에 이를 'test[x]' 즉, 배열처럼 사용하고 있음
* 이처럼 인덱스를 사용하면 클래스를 배열처럼 운영할 수 있음
* 2차원 배열 혹은 그 이상에서의 인덱스 사용 코드
```C#
class StudentScore
{
  //2차원 배열 선언과 초기값 배정
  private double[ , ] eachScore = new double[3,3] { {0,0,0}, {0,0,0}, {0,0,0} };

  //매개변수를 두 개 가지는 인덱서
  public double this[int x, int y]
  {
    set { eachScore[x,y] = value; }
    get { return eachScore[x,y]; }
  }

  //과목 선택을 위해 1차원 배열 사용
  private string[] subject = new string[3] { "국어, "영어", "수학" };

  //매개변수를 한 개 가지는 인덱서 : 인덱서 오버로딩
  public string this[int z]
  {
    set { subject[z] = value; }
    get { return subject[2]; }
  }
}

class Program
{
  static void Main()
  {
    int a; //학생 카운터
    int b; //과목별 점수
    double sum = 0.0; //총점
    double avg = 0.0; //평균

    //클래스의 인스턴스 생성
    StudentScore ss = new StudentScore();

    for(b = 0; b < 3; b++)
    {
      for(a = 0; a < 3; a++)
      {
        //과목을 고정시킨 채 학생을 바꾸면서 입력을 받는다.
        Console.Write("학생{0}의 {1} 성적을 입력하세요: ", a, ss[b]);
        ss[a, b] = Convert.ToDouble(Console.ReadLine());
      }
    }

    Console.WriteLine();

    //학생을 고정시킨 채 과목을 바꾸면서 계산한다.
    for(a = 0; a < 3; a++)
    {
      for(b = 0; b < 3; b++)
      {
        sum += ss[a, b];
        avg = sum / 3;
      }

      Console.WriteLine("학생{0}의 국영수 총점은 {1}점입니다", a, sum);
      sum = 0; //총점 초기화

      Console.WriteLine("학생{0}의 국영수 평균은 {1}점입니다", a, avg);
    }
  }
}
```
* 함수의 오버로딩과 마찬가지로 시그니처까지 똑같은 인덱서는 만들 수 없음
* 외부 클래스에서 접근하여 임의로 수정하는 것이 불가능함(캡슐화 되어 있다는 뜻!)

### 인덱스 vs. 인덱서
* 배열에서 데이터가 저장되는 위치(주소)를 가리키는 변수를 **인덱스(index)** 라고 하고,
* **인덱서(indexer)** 는 특별한 종류의 프로퍼티를 부르는 이름임

</div>
</details>

___

<details>
<summary>2. 열거형 클래스</summary>
<div markdown="1">       

</div>
</details>
