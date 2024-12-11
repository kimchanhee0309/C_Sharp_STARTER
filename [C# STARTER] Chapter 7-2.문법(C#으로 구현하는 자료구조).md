# 큐(Queue)

* FIFO(First In, First Out). 즉, 먼저 들어온 자료가 먼저 나간다는 의미
* **Enqueue** : 큐에 데이터를 삽입하는 행위
* **Dequeue** : 큐에서 데이터를 삭제하는 행위
* Enqueue는 맨 마지막에 입력한 자료를 대상으로 이루어지지만, Dequeue는 맨 처음에 입력한 자료를 대상으로 한다는 점이 스택과 다름
* 순차적으로 처리해야 하는 경우에 유용하게 사용됨
* 스택과 마찬가지로 큐에 저장되는 모든 자료는 같은 자료형을 가져야 함
* 스택과 마찬가지로 메모리 공간이 자동적으로 증가하는 동적 자료구조를 갖음
* 'System.Collections.Generic'을 호출해야 한다는 점도 스택과 같음
> Queue<자료형> = new Queue<자료형>();

프로퍼티와 함수 | 기능 
----------------- | ------------------ 
Count | 큐에 저장된 데이터의 총수를 반환한다.
Peek() | 큐에 저장된 마지막 데이터가 무엇인지 확인한다. 그러나 삭제는 하지 않는다.
Dequeue() | 큐에 저장된 맨 처음 자료가 무엇인지 확인하고 해당 데이터를 삭제한다.
Enqueue(T t) | 큐의 맨 위에 데이터를 삽입한다.
Clear() | 큐에 저장된 모든 데이터를 삭제한다.
Contains(T t) | 주어진 데이터가 큐에 존재하면 true, 존재하지 않으면 false 값을 반환한다.
ToArray() | 큐에 저장된 데이터들을 새로운 배열로 만들어 복사한다.
TrimExcess() | 사용하지 않은 메모리 공간을 정리한다.

* 예시 코드
```C#
using System;
using Syste.Collections.Generic;

namespace QueueDemo
{
  class Program
  {
    static void Main()
    {
      //새로운 큐의 인스턴스를 생성한다.
      Queue<char> qu = new Queue<char>();

      qu.Enqueue('A');
      qu.Enqueue('B');
      qu.Enqueue('C');

      Console.WriteLine(qu.Count + "개의 자료가 있습니다.\n");
      Console.Write("맨 위에 있는 값은 " + qu.Peek() + "입니다.\n");
      Console.Write("맨 위에 있는 값 " + qu.Dequeue() + "을 삭제합니다.\n");

      Console.WriteLine("\n----------");

      Console.WriteLine(qu.Count + "개의 자료가 있습니다.\n");
      Console.Write("맨 위에 있는 값은 " + qu.Peek() + "입니다.\n");

      Console.WriteLine("\n----------");

      foreach (char c in qu)
      {
        Console.Write(c + " ");
      }

      Console.WriteLine("\n----------");

      qu.Enqueue('D');
      qu.Enqueue('E');

      Console.WriteLine(qu.Count + "개의 자료가 있습니다.\n");
      Console.Write("맨 위에 있는 값은 " + qu.Peek() + "입니다.\n");

      Console.WriteLine("\n----------");

      foreach (char c in qu)
      {
        Console.Write(c + " ");
      }

      qu.TrimExcess(); //사용하지 않는 메모리 공간을 정리한다.

      Console.WriteLine("\n----------");

      if (qu.Contains('B'))
      {
        qu.Clear();
      }

      Console.WriteLine(qu.Count + "개의 자료가 있습니다.\n");
    }
  }
}
```
