# 딕셔너리(Dictionary)

* 딕셔너리(Dictionary)는 **키(Key)** 와 **자료(value)** 의 쌍으로 이루어짐
* 키는 딕셔너리에 저장된 데이터에 접근하는 열쇠로 사용됨
* So, 똑같은 값을 가지는 키는 존재할 수 없음
* 사용하기 위해서는 저장하는 모든 자료들이 같은 자료형을 가져야 함
* 같은 값을 갖는 키는 존재할 수 없지만, 같은 값을 갖는 자료는 존재할 수 있음
* 정렬된 리스트(SortedList)와 딕셔너리(Dictionary)의 차이점
  * 정렬된 리스트에 비해 딕셔너리가 정렬되지 않은 자료에 대한 삽입 및 삭제 연산을 더 빠르게 처리함
  * 한 번 데이터가 정렬되어진 뒤에는 정렬된 리스트가 딕셔너리에 비해 더 빠른 작업 속도를 가짐
  * 정렬된 리스트는 딕셔너리에 비해 일반적으로 더 적은 메모리 공간을 사용함. But, DB 관리나 캐쉬 메모리 관리에는 정렬된 리스트보다 딕셔너리가 더 좋은 성능을 보임

프로퍼티와 함수 | 기능 
----------------- | ------------------ 
Count | 딕셔너리 안에 존재하는 모든 키/자료 쌍의 총수를 반환한다.
Values | 딕셔너리 안에 존재하는 데이터의 값을 순서대로 반환한다.
keys | 주어진 키값에 상응하는 데이터값을 반환한다.
Add(key, value) | 주어진 키/자료의 쌍을 딕셔너리에 추가한다.
Remove(key) | 주어진 키값을 가진 자료를 딕셔너리에서 삭제한다.
Clear() | 딕셔너리에 존재하는 모든 데이터를 삭제한다.
Containskey(key) | 딕셔너리에 해당 키값이 있으면 true, 없으면 false 값을 반환한다.
ContainsValue(value) | 딕셔너리에 해당 데이터값이 있으면 true, 없으면 false 값을 반환한다.

> Dictionary<키 자료형, 데이터 자료형> =
> new Dictionary<키 자료형, 데이터 자료형>();

* 예시 코드
```C#
using System;
using System.Collections.Generic;

namespace DictionaryDemo
{
  class Program
  {
    static voind Main()
    {
      //새로운 딕셔너리의 인스턴스를 생성한다.
      Dictionary<int, string> dn = new Dictionary<int, string>();

      dn.Add(1, "Jeff Bezos");
      dn.Add(2, "Larry Page");
      dn.Add(3, "Mark Zuckerberg");
      dn.Add(4, "Warren Buffett");

      Console.WriteLine(dn.Count + "개의 자료가 있습니다.\n");

      //아래 dn.Values 와 비교할 것
      foreach (int i in dn.Keys)
      {
        Console.WriteLine(dn[i]);
      }

      Console.WriteLine("\n----------");

      if (dn.ContainsKey(5))
      {
        dn.Clear();
      }
      else
      {
        dn.Add(5, "Elon Musk");

        //위의 dn.Keys와 비교할 것
        foreach(string s in dn.Values)
        {
          Console.WriteLine(s);
        }
      }

      Console.WriteLine("\n----------");

      Console.WriteLine(dn.Count + "개의 자료가 있습니다.\n");

      if (dn.ContainsValue("Elon Musk"))
      {
        dn.Remove(1);

        foreach (string s in dn.Values)
        {
          Console.WriteLine(s);
        }
      }

      Console.WriteLine("\n----------");

      Console.WriteLine(dn.Count + "개의 자료가 있습니다.\n");
    }
  }
}
```
