# 해쉬셋(HashSet)

* 중복값을 가질 수 없는 특별한 자료구조
* 해쉬셋의 모든 데이터 역시 같은 자료형을 가져야 함
* 딕셔너리와 달리 인덱스를 가지지 않기 때문에 주소를 이용한 데이터 접근과 정렬이 불가능함
* 해쉬셋을 쓰는 이유
  * DB 관련 프로그래밍에 자주 사용됨
  * 빠른 검색 능력과 빠른 데이터의 추가 및 삭제가 가능하기 때문에 메모리 관리에 가장 많이 사용됨
> HashSet<자료형> = new HashSet<자료형>();

프로퍼티와 함수 | 기능 
----------------- | ------------------ 
Count | 해쉬셋에 저장된 데이터의 총수를 반환한다.
Add(T t) | 제시한 데이터를 해쉬셋에 추가한다.
Remove(T t) | 제시한 데이터를 해쉬셋에서 삭제한다.
Clear() | 해쉬셋의 모든 데이터를 삭제한다.
Contains(T t) | 주어진 데이터가 해쉬셋에 있으면 true, 없으면 false 값을 반환한다.
IsSubsetOf(ICollection c) | 이 해쉬셋이 지정한 해쉬셋의 부분집합이라면 true, 아니면 false 값을 반환한다.
IsSupersetOf(ICollection c) | 이 해쉬셋이 지정한 해쉬셋을 포함하는 상위 집합이라면 true, 아니면 false 값을 반환한다.
IntersectWith(ICollection c) | 현재의 해쉬셋을 기준으로 지정한 해쉬셋과의 교집합을 반환한다.
ExceptWith(ICollection c) | 현재의 해쉬셋을 기준으로 지정한 해쉬셋과의 차집합을 반환한다.
UnionWith(ICollection c) | 이 해쉬셋과 지정한 해쉬셋을 병합한다. 단, 중복된 값이 있다면 자동으로 하나를 삭제한다.
TrimExcess() | 사용하지 않은 메모리 공간을 정리한다.

* 예시 코드
```C#
using System;
using System.Collections.Generic;

namespace HashSetDemo
{
  class Program
  {
    static void Main(string[] args)
    {
      HashSet<char> hs1 = new HashSet<char>();

      hs1.Add('A');
      hs1.Add('B');
      hs1.Add('C');

      Console.WriteLine("hs1에는 {0]개의 자료가 있습니다.", hs1.Count);

      HashSet<char> hs2 = new HashSet<char>();

      hs2.Add('A');
      hs2.Add('B');
      hs2.Add('C');
      hs2.Add('D');
      hs2.Add('E'); //동일한 자료의 입력은 허용되지 않음
      hs2.Add('E'); //단, 컴파일 시 오류 없이 자동적으로 입력이 무시됨
      hs2.Add('F');

      Console.WriteLine("hs2에는 {0}개의 자료가 있습니다.", hs2.Count);

      Console.WriteLine("----------");

      Console.WriteLine(hs1.IsSubsetOf(hs2));
      Console.WriteLine(hs1.IsSupersetOf(hs2));

      Console.WriteLine("----------");

      hs1.IntersectWith(hs2);

      Console.WriteLine("교집합 생성 이후 hs1에는 {0}개의 자료가 있습니다.", hs1.Count);

      foreach (char c in hs1)
      {
        Console.WriteLine(c);
      }

      Console.WriteLine("----------");

      hs2.ExceptWith(hs1);

      Console.WriteLine("차집합 생성 이후 hs2에는 {0}개의 자료가 있습니다.", hs2.Count);

      foreach (char c in hs2)
      {
        Console.WriteLine(c);
      }

      Console.WritELine("----------");

      hs1.UnionWith(hs2);

      Console.WriteLine("hs1과 hs1 병합 이후 hs1에는 {0}개의 자료가 있습니다.", hs1.Count);

      foreach (char c in hs1)
      {
        Console.WriteLine(c);
      }

      hs1.TrimExcess(); //사용하지 않는 메모리 공간을 정리한다.
      hs2.TrimExcess(); //사용하지 않는 메모리 공간을 정리한다.
    }
  }
}
```
