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

</div>
</details>

___

<details>
<summary>4. 불규칙 배열</summary>
<div markdown="1">       

</div>
</details>

___

<details>
<summary>5. 배열 프로퍼티와 집계 함수</summary>
<div markdown="1">       

</div>
</details>
