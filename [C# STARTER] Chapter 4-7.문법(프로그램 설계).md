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
    Console.Wirte("Give me any integer: ");
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
