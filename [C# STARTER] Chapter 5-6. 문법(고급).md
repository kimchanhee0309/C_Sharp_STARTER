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
</div>
</details>

___

<details>
<summary>12. 리스트(List)</summary>
<div markdown="1">       

</div>
</details>
