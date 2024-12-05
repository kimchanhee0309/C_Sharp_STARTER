# 제네릭, 리스트

<details>
<summary>11. 제네릭(generic)</summary>
<div markdown="1">       

### 제네릭 자료형
* 자료 입력의 형태를 제한해야 하는 경우도 있지만, 자료의 입력에 따라 프로그램이 반응해야 하는 경우도 존재함
* 이때 사용하는 것이 바로 **제네릭(generic)**
* **제네릭 자료형(generic type)** 을 사용하면 클래스에서 사용할 자료의 형식을 클래스 내부가 아닌 `외부`에서 정하게 됨
  * 즉, 입력값에 따라 그때 그떄 자료형이 정해지는 것임
  * 하나의 연산을 위해 만들어진 코드를 여러 다른 자료형의 입력에도 재사용할 수 있는 편리함이 생김
* 예시 코드
```C#
static int[] ArrayCopy(int[] src)
{
  int[] trg = new int[src.Length];

  for(int i = 0; i < src.Length; i++)
  {
    trg[i] = src[i];
  }

  return trg;
}

static void Main()
{
  int[] arr1 = new int[3];

  for(int i = 0; i < 3; i++)
  {
    Console.Write("정수를 입력하세요: ");
    arr[i] = Convert.ToInt32(Console.ReadLine());
  }

  int[] arr2 =  ArrayCopy(arr1);

  Console.WriteLine();

  for(int i = 0; i < arr2.Length; i++)
  {
    Console.WriteLine(arr2[i]);
  }
}
```
### 제네릭 클래스
* 자료를 적재하고자 할 때 주로 쓰임
* 예시 코드
```C#
class GenClass<T> //클래스를 제네릭으로 선언하고 있다.
{
  int index = 0; //멤버 변수 모두가 제네릭으로 선언되어야 하는 것은 아니다.
  T[] TArray = new T[10];

  public void Push(T item) //함수의 매개변수를 제네릭으로 선언하고 있다.
  {
    TArray[index++] = item; //입력을 받은 후 인덱스 값을 1 증가시킨다.
  }

  public T Pop(int x) //함수의 반환값을 제네릭으로 선언하고 있다.
  {
    return TArray[x];
  }
}

class Program
{
  static void Main()
  {
    //인스턴스를 생성할 때 원하는 자료형을 밝혀야 한다.
    GenClass<int> intArray = new GenClass<int>();
    GenClass<char> charArray = new GenClass<char>();

    intArray.Push(3);
    intArray.Push(6);
    charArray.Push('A');
    charArray.Push('B');

    Console.WriteLine("두 번째 입력값은 각각 {0}과 \'{1}\'입니다.",
                       intArray.Pop(1), charArray.Pop(1));
  }
}
```
* 클래스 자체를 제네릭으로 선언하면 해당 클래스는 최소 1개 이상의 제네릭 멤버를 가져야 함
* 클래스의 인스턴스를 생성할 때 원하는 자료형을 선언함
* 제네릭은 변ㅂ수나 함수뿐만 아니라 클래스와 인터페이스에도 두루 사용할 수 있음
</div>
</details>

___

<details>
<summary>12. 리스트(List)</summary>
<div markdown="1">       

### 리스트
### 정렬된 리스트
</div>
</details>
