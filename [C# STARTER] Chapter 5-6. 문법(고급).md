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
* 배열과의 차이점
  * 배열에 비해 **자료의 입출력이 더 역동적**이고, **크기를 자유자재로 조절**할 수 있음
  * 다양한 프로퍼티 및 함수를 포함하고 있기 때문에 배열에 비해 훨씬 효율적인 데이터 및 자원 관리가 가능함
* 리스트 또한 인스턴스를 생성한 뒤 사용 가능함
  > List<자료형> 리스트명 = new List<자료형>();

* 예시 코드
```C#
using System;
using System.Collections.Generic;

namespace ListDemo_1
{
  class Program
  {
    static void Main()
    {
      //리스트의 인스턴스를 생성한다. 이때 자료형을 함께 제시한다.
      List<int> li = new List<int>();

      //입력값이 없으므로 현재 리스트의 크기는 '0'이다.
      Console.WriteLine("현재 리스트의 크기는 " + li.Capacity + " 입니다.");
      Console.WriteLine("현재 리스트에는 " + li.Count + "개의 자료가 있습니다.\n");

      li.Add(1);

      //입력이 시작되면 리스트의 크기는 '4'로 증가한다.
      Console.WriteLine("현재 리스트의 크기는 " + li.Capacity + " 입니다.");
      Console.WriteLine("현재 리스트에는 " + li.Count + "개의 자료가 있습니다.\n");

      li.Add(3);
      li.Add(5);
      li.Add(12);
      li.Add(43);  //5번째 입력 자료, 리스트의 크기는 4에서 8로 증가한다.

      Console.WriteLine("현재 리스트의 크기는 " + li.Capacity + " 입니다.");
      Console.WriteLinie("현재 리스트에는 " + li.Count + "개의 자료가 있습니다.\n");
    }
  }
}
```
프로퍼티와 함수 | 기능 
----------------- | ------------------ 
Count | 리스트에 저장된 자료가 몇 개인지 세는 프로퍼티 
Capacity | 해당 리스트가 가질 수 있는 자료의 최대 수를 보여주는 프로퍼티
Clear | 리스트 안에 있는 모든 자료를 삭제하는 함수
TrimExcess() | 초과하여 할당한 메모리를 반환하는 함수, 모든 자료의 입력이 끝난 뒤 반드시 실행해주는 것이 좋음(크기 줄여줌)
Sort() | 리스트 안에 저장된 자료를 오름차순으로 정렬하는 함수
Reverse() | 리스트 안에 저장된 자료의 저장 순서를 반대로 바꾸는 함수
ToArray() | 리스트 안에 있는 자료들을 새로운 배열을 복사하는 함수
Add(T t) | 리스트에 자료를 추가하는 함수
AddRange(리스트명) | 리스트 안에 저장된 모든 자료를 리스트의 마지막에 복사하여 추가하는 함수
Insert(int i, T t) | 주어진 위치에 주어진 자료를 추가하는 함수, 리스트의 마지막에 자료를 추가하는 Add(T t)와는 다름
InsertRange(int i, 리스트명) | 주어진 위치에 주어진 위치 직전까지의 모든 자료를 복사하여 추가하는 함수
Remove(T t) | 리스트를 검색하여 주어진 값을 찾아 삭제하는 함수. 중복 값은 맨 처음 찾은 값 하나만 삭제됨, 크기까지 줄어들진 않음
RemoveAt(index) | 주어진 인덱스 위치의 자료를 삭제하는 함수
RemoveRange(index, count) | 주어진 인덱스 위치부터 count에 의해 주어진 개수만큼 자료를 삭제하는 함수
Contain(T t) | 주어진 값이 리스트에 저장되어 있는지 확인하는 함수. 존재하면 true, 아니면 false 값 반환
IndexOf(T t) | 주어진 겂이 처음 저장된 위치값(인덱스)을 반환하는 함수

* 예시 코드
```C#
using System;
using System.Collections.Generic;

namespace ListDemo_2
{
  class Program
  {
    static void Main()
    {
      List<string> li = new List<string>();

      Console.WriteLine("현재 리스트에는 " + li.Count + "개의 자료가 있습니다.");
      Console.WriteLine("현재 리스트의 크기는 " + li.Capacity + "입니다.\n");

      li.Add("James");

      Console.WriteLine("현재 리스트에는 " + li.Count + "개의 자료가 있습니다.");
      Console.WriteLine("현재 리스트의 크기는 " + li.Capacity + "입니다.\n");

      li.Add("Andrew");
      li.Add("George");
      li.Add("Donald");
      li.Add("John");

      Console.WriteLine("현재 리스트에는 " + li.Count + "개의 자료가 있습니다.");
      Console.WriteLine("현재 리스트의 크기는 " + li.Capacity + "입니다.\n");

      li.TrimExcess(); //불필요한 공간을 정리한다.

      Console.WriteLine("현재 리스트에는 " + li.Count + "개의 자료가 있습니다.");
      Console.WriteLine("현재 리스트의 크기는 " + li.Capacity + "입니다.\n");

      li.Add("Susan");
      li.Add("Louisa");
      li.Add("Dolley");
      li.Add("Clara");
      li.Add("Ansel");
      li.ADd("Grace");

      Console.WriteLine("현재 리스트에는 " + li.Count + "개의 자료가 있습니다.");
      Console.WriteLine("현재 리스트의 크기는 " + li.Capacity + "입니다.\n");

      li.Remove("Ansel"); //입력 자료 중 "Ansel"를 찾아 삭제한다.

      //리스트에 들어있는 자료를 순차적으로 출력한다. 배열을 사용하는 것과 다르지 않다.
      for (int x = 0; x < li.Count; x++)
      {
        Console.WriteLine(li[x]);
      }

      li.RemoveAt(2); //리스트의 3번째 자료를 삭제한다.
      li.TrimExcess(); //불필요한 공간을 정리한다.

      Console.WriteLine("현재 리스트에는 " + li.Count + "개의 자료가 있습니다.");
      Console.WriteLine("현재 리스트의 크기는 " + li.Capacity + "입니다.\n");

      for (int x = 0; x < li.Count; x++)
      {
        Console.WriteLine(li[x]);
      }

      li.InserRange(3, li); //리스트의 3번째까지 자료를 4번째부터 복사해 붙여 넣는다.

      Console.WriteLine("현재 리스트에는 " + li.Count + "개의 자료가 있습니다.");
      Console.WriteLine("현재 리스트의 크기는 " + li.Capacity + "입니다.\n");

      for (int x = 0; x < li.Count; x++)
      {
        Console.WriteLine(li[x]);
      }

      Console.WriteLine();

      li.RemoveRange(5, 5); //6번째 자료부터 이어지는 5개의 자료를 삭제한다.
      li.TrimExcess(); //불필요한 공간을 정리한다.
      li.Sort(); //리스트에 있는 자료를 오름차순으로 정렬한다.

      for (int x = 0; x < li.Count; x++)
      {
        Console.WriteLine(li[x]);
      }

      Console.WriteLine("현재 리스트에는 " + li.Count + "개의 자료가 있습니다.");
      Console.WriteLine("현재 리스트의 크기는 " + li.Capacity + "입니다.\n");

      li.Add("Henry");

      Console.WriteLine("현재 리스트에는 " + li.Count + "개의 자료가 있습니다.");
      Console.WriteLine("현재 리스트의 크기는 " + li.Capacity + "입니다.\n");

      Console.WriteLine(li[8]); //리스트의 9번째 자료를 출력한다.
    }
  }
}
```
### 정렬된 리스트
* 특징
  * **'키'** 와 **'자료'** 를 한 묶음으로 저장함
  * 자료의 입출력과 검색 속도를 한층 더 향상시킬 수 있음
  * 정렬된 리스트에 저장한 자료는 키(Key)를 통해서 접근함
  * 저장할 자료들은 모두 동일한 자료형을 가져야 하며, 키에 대한 복제는 허용되지 않음
  * 즉, 리스트 안의 모든 키값은 유일한 값이어야 한다는 뜻, 키값은 'null'일 수가 없음
  * 최초 선언시 자료형을 함께 선언할 수도 있고 나중에 따로 선언할 수도 있음
* 마찬가지로 사용하기 위해서는 인스턴스를 생성해주어야 함
  > 방법1.
  > SortedList 리스트명 = new SortedList();
  >
  > 방법2.
  > SortedList<키, 자료형> 리스트명 = new SortedList<키, 자료형>();

* 예시 코드
```C#
using System;
using System.Collections; //자료형의 나중에 선언하는 경우 필요
using System.Collections.Generic; //자료형을 함께 선언하는 경우 필요

namespace SortedListDemo_1
{
  class Program
  {
    static void Main()
    {
      //입력할 자료형을 정하지 않고 있다.
      //아래와 같은 형식을 사용하려면 <Using System.Collections>가 필요
      SortedList sl_1 = new SortedList();

      sl_1.Add(1, 100); //이처럼 자료형에 상관없이 저장이 가능함
      sl_1.Add(2, "James");
      sl_1.Add(3, 3.14);

      //입력할 자료형을 정하고 있다.
      //아래와 같은 형식을 사용하려면 <using System.Collections.Generic)이 필요
      SortedList<int, string> sl_2 = new SortedList<int, string>();

      //이 경우, 정의한 자료형<정수형, 문자열형)만 입력할 수 있음
      sl_2.Add(9, "Microsoft");

      //입력된 자료가 하나지만 정확한 키값인 '9'를 적어준다.
      Console.WriteLine(sl_2[9]);
    }
  }
}
```

프로퍼티와 함수 | 기능 
----------------- | ------------------ 
Count | SortedList에 저장된 자료가 몇 개인지 세는 프로퍼티
Capacity | 해당 SortedList가 가질 수 있는 자료의 최대 수를 보여주는 프로퍼티
IsFixedSize | 해당 SortedList가 고정된 크기인지 보여주는 프로퍼티(true / false)
IsReadOnly | 해당 SortedList가 읽기전용인지 보여주는 프로퍼티(true / false)
Keys[index] | 주어진 인덱스 위치의 키값을 보여주는 프로퍼티 : SortedList를 선언할 때 자료형이 미리 정의한 경우에만 사용할 수 있음
Values[index] | 주어진 인덱스 위치의 자료값을 보여주는 프로퍼티 : SortedList를 선언할 때 자료형이 미리 정의한 경우에만 사용할 수 있음
Add(key, value) | 주어진 (key, value) 쌍의 값을 SortedList에 추가하는 함수
Remove(value) | 주어진 자료값을 검색하여 주어진 값을 찾아 삭제하는 함수. 단, 맨 처음 찾은 값 하나만 삭제
RemoveAt(index) | 주어진 인덱스 위치의 자료를 삭제하는 함수
ContainsKey(key) | 주어진 키값이 SortedList에 존재하는지 보여주는 함수(true/false)
ContainsValue(value) | 주어진 자료가 SortedList에 존재하는지 보여주는 함수(true/false)
GetKey(index) | 주어진 인덱스 위치의 키값을 반환하는 함수
GetByIndex(index) | 주어진 인덱스 위치의 자료값을 반환하는 함수
IndexOfKey(key) | 주어진 키값이 저장된 위치(인덱스)를 반환하는 함수
IndexOfValue(value) | 주어진 자료값이 처음 저장된 위치(인덱스)를 반환하는 함수
Clear() | SortedList 안에 있는 모든 자료를 삭제하는 함수
TrimExcess() | 초과하여 할당한 메모리를 반환하는 함수

* 예시 코드
```C#
using System;
using System.Collections;
using System.Collections.Generic;

namespace SortedListDemo_1
{
  class Program
  {
    static void Main()
    {
      SortedList sl_1 = new SortedList();

      Console.WriteLine("현재 리스트에는 " + sl_1.Count + "개의 자료가 있습니다.");
      Console.WriteLine("현재 리스트의 크기는 " + sl_1.Capacity + " 입니다.\n");

      sl_1.Add(1, 100);
      sl_1.Add(23, "James");
      sl_1.Add(456, 3.14);

      Console.WriteLine("현재 리스트에는 " + sl_1.Count + "개의 자료가 있습니다.");
      Console.WriteLine("현재 리스트의 크기는 " + sl_1.Capacity + " 입니다.\n");

      for (int i = 0; i < sl_1.Count; i++)
      {
        Console.WriteLine("SortedList.Values[{0}] = {1}", i, sl_1[i]);
      }

      Console.WriteLine(sl_1.ContainsKey(23));
      Console.WriteLine(sl_1.ContainsValue(3.14) + "\n");

      sl_1.Add(321, "Moon");
      sl_1.Add(123, A);
      sl_1.Add(234, "Hello World");

      Console.WriteLine("현재 리스트에는 " + sl_1.Count + "개의 자료가 있습니다.");
      Console.WriteLine("현재 리스트의 크기는 " + sl_1.Capacity + " 입니다.\n");

      for (int i = 0; i < sl_1.Count; i++)
      {
        Console.WriteLine("GetKey({0}) = {1}", i, sl_1.GetKey(i));
      }

      Console.WriteLine();

      for (int i = 0; i < sl_1.Count; i++)
      {
        Console.WriteLine("GetByIndex({0}) = {1}", i, sl_1.GetByIndex(i));
      }

      Console.WriteLine();

      SortedList<int, string> sl_2 = new SortedList<int, string>();

      sl_2.Add(3, "MicroSoft");
      sl_2.Add(123, "Samsung");
      sl_2.Add(234, "SpaceX");

      Console.WriteLine("123 키값을 가진 자료의 위치는 " + sl_2.IndexOfKey(123) + " 입니다.");
      Console.WriteLine("Samsung의 자료 위치는 " + sl_2.IndexOfValue("Samsung") + " 입니다.\n");

      sl_2.TrimExcess();

      Console.WriteLine("현재 리스트에는 " + sl_2.Count + "개의 자료가 있습니다.");
      Console.WriteLine("현재 리스트의 크기는 " + sl_2.Capacity + " 입니다.\n");

      for (int i = 0; i < sl_2.Count; i++)
      {
        Console.WriteLine("SortedList.Keys[{0}] = {1}", i, sl_2.Keys[i]);
      }

      Console.WriteLine();

      for (int i = 0; i < sl_2.Count; i++)
      {
        Console.WriteLine("SortedList.Values[{0}] = {1}", i, sl_2.Values[i]);
      }
    }
  }
}
```

</div>
</details>
