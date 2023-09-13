# 배열

<details>
<summary>1. 배열 선언과 값 배정</summary>
<div markdown="1">       

* **배열(array)** 은 하나의 자료가 아닌 '일련의 자료'를 저장하기 위해 사용하는 자료구조임
* 즉, 같은 자료형을 가지는 여러 변수들의 집합을 뜻함
* 배열이 일반 변수와 다른 점
  * 배열을 선언하는 방법이 클래스의 인스턴스를 만들 때처럼 `new 키워드`를 사용한다는 점
    >자료형 [ ] 배열명 = new 자료형[크기];
* 배열에 값을 저장하는 방법
  * 원하는 값을 원하는 장소에 저장하는 방식
    >int[] studentIDs = new int[5];
    >
    >studentIDs[0] = 55;
  * 일련의 자료를 한 번에 저장하는 방식
    >int[] studentIDs = new int[5] { 1, 2, 3, 4, 5 };
```C#
static void Main()
{
  //배열의 선언
  int[] evenNums = new int[10];

  for(int x = 0; x < 10; x++)
  {
    //배열에 데이터 입력(저장)
    evenNums[x] = x * 2;

    //배열에 저장된 데이터 출력
    Console.WriteLine("You just saved {0}", evenNums[x]);
  }
}
```
```C#
static void Main()
{
  //배열의 선언과 초기값 배정
  int[] myIntegers = new int[5] { 1, 2, 3, 4, 5 };

  for(int i = 0; i< 5; i++)
  {
    //배열에 저장된 데이터 출력
    Console.WriteLine("Saved number is {0}", myIntegers[i]);
  }

  for(int i = 0; i < 5; i++)
  {
    //사용자 입력을 배열에 저장
    Console.Write("Give me any integer: ");
    myIntegers[i] = Convert.ToInt32(Console.ReadLine());
  }

  for(int i = 0 ; i < 5; i++)
  {
    //배열에 저장된 데이터 출력
    Console.WriteLine("The number you just saved is {0}", myIntegers[i]);
  }
}
```
</div>
</details>

___

<details>
<summary>2. foreach 문</summary>
<div markdown="1">       

* **foreach문** : 배열의 특화된 반복문
  >foreach(자료형 변수명 in 배열명)
  >
  >{
  >
  >  statement(s)...
  >
  >}
* foreach 문 특징
  * 일반적인 반복문이 가지는 카운터를 가지지 않음
  * 대신, foreach 문은 자신만의 변수를 가지게 됨
    * 이것은 foreach 문이 배열에 저장된 데이터값을 찾아내어 그것을 자신의 변수에 담아 나오는 방식으로 작동하기 때문임
    * So, foreach 문에서 **선언한 변수**와 **배열에 저장된 데이터의 자료형**이 서로 **일치**해야만 함
  * 특히 배열에 저장된 데이터가 총 몇 개인지 알 수 없을 때 진가를 발휘함
    * foreach 문 스스로 데이터가 저장된 부분의 끝까지 반복문을 실행하기 때문임
    * So, 다른 반복문과 달리 **종료 조건을 제시하지 않음**
* 예시
```C#
static void Main()
{
  int[] myIntegers = new int[10];
  int sum = 0;

  for(int x = 0; x < 5; x++)
  {
    Console.Write("정수를 입력하세요: ");
    myIntegers[x] = Convert.ToInt32(Console.ReadLine());
  }

  /* foreach 문에는 반복문의 종료 조건이 주어지고 있지 않고
     myIntegers 뒤에 배열을 표시하는 []가 붙어 있지 않다 */
  foreach(int y in myIntegers)
  {
    sum += y;
  }

  Console.WriteLine("입력한 모든 숫자의 합은 {0}입니다." sum);
}
```
* 최초 선언된 배열의 크기는 '10'이지만, 실제로는 5개의 자료만 입력하고 잇음
* 그럼에도 불구하고 foreach 문은 오류 없이 저장된 데이터를 모두 가져옴

```C#
static void Main()
{
  string[] studentNames = new string[10];

  for(int x = 0; x < 5; x++)
  {
    Console.Write("학생의 이름을 입력하세요: ");
    studentNames[x] = Console.ReadLine();
  }

  //foreach 문은 카운터를 가지지 않는다.
  foreach(int y in studentNames)
  {
    //foreach 문의 변수를 카운터처럼 사용하고 있다 : 오류의 원인
    Console.WriteLine("The name saved in array is {0}", studentNames[y]);
  }
}
```
* foreach 문의 변수를 일반 반복문의 카운터처럼음
</div>
</details>

___

<details>
<summary>3. 2차원 배열</summary>
<div markdown="1">       

* 열과 행을 가진 구조로 저장하는 방식
* 각 셀은 두 개씩의 **인덱스(index)** 를 가지게 됨
* 앞에 있는 인덱스가 `행(row)`, 뒤에 있는 인덱스가 `열(column)`을 가리킴
* 2차원 배열에 데이터를 저장하는 방법
```C#
static void Main()
{
  //2차원 배열 선언(2개의 행과 4개의 열)
  double[ , ] eachScore = new double[2, 4];

  //2차원 배열에 데이터를 입력하고 있다.
  eachScore[0, 0] = 2.43;
  eachScore[0, 1] = 3.01;
  eachScore[0, 2] = 9.47;
  eachScore[1, 0] = 8.36;

  foreach(double d in eachScore)
  {
    Console.WriteLine(d);
  }
}
```
* 아무런 값을 배정하지 않은 주소에는 0이 입력됨
* 즉, 2차원 배열은 하나의 행을 하나의 데이터처럼 인식한다는 것을 알 수 있음
* 2차원 배열을 선언할 때 초기값을 배정하는 방법
```C#
static void Main()
{
  //2차원 배열 선언과 초기값 배정
  double[ , ] eachScore = new double[3,3] { {0,0,0}, {0,0,0}, {0,0,0} };

  //과목 선택을 위해 1차원 배열 사용
  string[] subject = new string[3] { "국어", "영어", "수학" };

  int a; //학생 카운터
  int b; //과목별 점수
  double sum = 0.0; //총점
  double avg = 0.0; //평균

  for(b = 0; b < 3; b++)
  {
    for(a = 0; a < 3; a++)
    {
      //과목을 고정시킨 채 학생을 바꾸면서 입력을 받는다.
      Consle.Write("학생{0}의 {1} 성적을 입력하세요: ", a, subject[b]);
      eachScore[a, b] = Convert.ToDouble(Console.ReadLine());
    }
  }

  Console.WriteLine();

  //학생을 고정시킨 채 과목을 바꾸면서 계산한다.
  for(a = 0; a < 3; a++)
  {
    for(b = 0; b < 3; b++)
    {
      sum += eachScore[a, b];
      avg = sum / 3;
    }

    Console.WriteLine("학생 {0}명의 국영수 총점은 {1}점입니다.", a, sum);
    sum = 0; //총점 초기화

    Console.WriteLine("학생 {0}명의 국영수 평균은 {1}점입니다.", a, avg);
  }
}
```
</div>
</details>

___

<details>
<summary>4. 불규칙 배열</summary>
<div markdown="1">       

* 2차원 배열이 가지는 약점
  * 각각의 행이 반드시 같은 수의 열을 가져야 한다는 것
  * 즉, 크기가 미리 정해져 있어야 한다는 뜻!
  * 이때 쓸 수 있는 것이 바로 `불규칙 배열(가변 배열)`임
  * 불규칙 배열은 크기가 서로 다른 여러 개의 1차원 배열을 묵어준 것과 같음
* 불규칙 배열 선언 방식
  >자료형 [][] 배열명 = new 자료형 [행의 개수][];
* 불규칙 배열을 선언할 때는 행의 개수만 명시할 뿐 열의 개수는 명시하지 않는다는 점 기억하기
* 학력을 저장하는 배열 코드
```C#
static void Main()
{
  //불규칙 배열 선언
  string[][] eduLevel = new string[3][];

  //학위 수준 선택을 위해 1차원 배열 사용
  string[] eduMajor = new string[4] { "고등학교 계열", "학사 전공", "석사 전공", "박사 전공" };

  int a; //사원 카운터
  int b; //사원별 배열의 크기(= 학위 수준)
  int c; //두 번째 for 문의 카운터

  for(a = 0; a < 3; a++)
  {
    Console.WriteLine("고졸:1\n학사:2\n석사:3\n박사:4");

    Console.WriteLine("-----------------------------------");
    Console.Write("사원{0}의 학위 수준을 입력하세요: ", a);

    //사원별 학위 수준이 곧 사원별 배열의 크기가 된다.
    b = Convert.ToInt16(Console.ReadLine());

    Console.WriteLine("-----------------------------------");

    //불규칙 배열을 사용하려면 각각 행을 1차원 배열로 선언해야 한다.
    eduLevel[a] = new string[b];

    for(c = 0; c < b; c++)
    {
      Console.Write("사원{0}의 {1}을 입력하세요: ", a, eduMajor[c]);
      eduLevel[a][c] = Console.ReadLine();
    }

    Console.WriteLine();
  }

  for(a = 0; a < 3; a++)
  {
    Console.Write("사원{0}의 전공은", a);

    //각 배열의 크기를 계산하기 위해 .Length 사용
    for(c = 0; c < eduLevel[1].Length; c++)
    {
      Console.Write(" {0}", eduLevel[a][c]);
    }

    Console.WriteLine("입니다.");
  }
}
```
* 불규칙 배열에 값을 입력하기에 앞서 각각의 행(row)을 1차원 배열로 선언해주어야 한다는 사실 잊지 말기!
</div>
</details>

___

<details>
<summary>5. 배열 프로퍼티와 집계 함수</summary>
<div markdown="1">       

 #### 배열 관련 프로퍼티
  
프로퍼티 | 기능 
------------ | ------------- 
IsFixedSize | 배열이 고정된 크기를 가졌는지 확인, 반환값 : 참or거짓 
IsReadOnly | 배열이 읽기전용인지 즉, 수정할 수 없는 지 확인, 반환값 : 참or거짓
Length | 배열의 크기를 확인, 반환값 : 32bit 정수값
LongLength | 배열의 크기를 확인, 반환값 : 64bit 정수값
Rank | 몇 차원 배열인지 확인

```C#
static void Main()
{
  //1차원 배열의 선언
  int[] arr1 = new int[5];
  Console.WriteLine("arr1.IsFixedSize = {0}", arr1.IsFixedSize);
  Console.WriteLine("arr1.IsReadOnly = {0}", arr1.IsReadOnly;
  Console.WriteLine("arr1.Length = {0}", arr1.Length);
  Console.WriteLine("arr1.LongLength = {0}", arr1.LongLength);
  Console.WriteLine("arr1.Rank = {0}", arr1.Rank);
  Console.WriteLine();

  //2차원 배열의 선언
  int[ , ] arr2 = new int[5,3];
  Console.WriteLine("arr2.IsFixedSize = {0}", arr2.IsFixedSize);
  Console.WriteLine("arr2.IsReadOnly = {0}", arr2.IsReadOnly;
  Console.WriteLine("arr2.Length = {0}", arr2.Length);
  Console.WriteLine("arr2.LongLength = {0}", arr2.LongLength);
  Console.WriteLine("arr2.Rank = {0}", arr2.Rank);
  Console.WriteLine();

  //불규칙 배열의 선언: 결과값을 눈여겨 보자
  string[][] arr3 = new string[5][];
  Console.WriteLine("arr3.IsFixedSize = {0}", arr3.IsFixedSize);
  Console.WriteLine("arr3.IsReadOnly = {0}", arr3.IsReadOnly;
  Console.WriteLine("arr3.Length = {0}", arr3.Length);
  Console.WriteLine("arr3.LongLength = {0}", arr3.LongLength);
  Console.WriteLine("arr3.Rank = {0}", arr3.Rank);
  Console.WriteLine();
}
```

#### 배열 관련 집계 함수

함수 | 기능 
------------ | ------------- 
배열명.Min() | 배열에 저장된 값 중 가장 작은 값을 반환한다.
배열명.Max() | 배열에 저장된 값 중 가장 큰 값을 반환한다.
배열명.Sum() | 배열에 저장된 값의 총합을 계산하여 반환한다.
배열명.Average() | 배열에 저장된 값의 평균을 계산하여 반환한다.
배열명.Count() | 배열에 저장된 데이터의 총 개수를 계산하여 반환한다.

```C#
using System;
using System.Linq;

namespace ArrayMethods
{
  class Program
  {
    static void Main()
    {
      int[] arr4 = new int[5] { 21, 98, 43, 27, 13 };

      Console.WriteLine("배열에서 가장 큰 수는 {0}입니다.", arr4.Max());
      Console.WriteLine("배열에서 가장 작은 수는 {0}입니다.", arr4.Min());
      Console.WriteLine("배열에 저장된 값의 총 합은 {0}입니다.", arr4.Sum());
      Console.WriteLine("배열에 저장된 값의 평균은 {0}입니다.", arr4.Average());
      Console.WriteLine("배열에 저장된 데이터의 개수는 {0}입니다.", arr4.Count());
    }
  }
}
```

</div>
</details>
