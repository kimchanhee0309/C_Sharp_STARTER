# 스택(Stack)
* LIFO(Last In, First Out) 즉, 마지막에 들어온 자료가 먼저 나간다는 의미
* **'Push'** : 스택에 자료를 삽입하는 것
* **'Pop'** : 스택에서 자료를 삭제하는 것
* Push 든 Pop 이든 맨 마지막에 입력한 자료를 대상으로 작업이 이루어짐
* 각종 프로그램에서 **실행 취소(undo)** 와 **다시 실행(redo)** 기능을 만들 때 가장 유용하게 사용되는 자료구조임
* 스택에 저장되는 모든 자료는 동일한 자료형을 가짐
* 자신이 사용하는 메모리의 공간을 자동으로 증가시킨다는 면에서 동적인 자료구조에 속함
* 'System.Collections.Generic'을 먼저 호출해야 한다는 점에서 리스트와 닮음
> Stack<자료형> = new Stack<자료형>();
  
프로퍼티와 함수 | 기능 
----------------- | ------------------ 
Count | 스택 안에 저장된 데이터의 총수를 반환한다.
Peek() | 스택에 저장된 마지막 데이터가 무엇인지 확인한다. 그러나 삭제는 하지 않는다.
Pop() | 스택에 저장된 마지막 데이터가 무엇인지 확인한 뒤 해당 데이터를 삭제한다.
Push(T t) | 스택의 맨 위에 새로운 데이터를 삽입한다.
Clear() | 스택에 저장된 모든 데이터를 삭제한다.
Contains(T t) | 주어진 데이터가 스택 안에 존재하면 true, 존재하지 않으면 false 값을 반환한다.
ToArray() | 스택 안에 있는 데이터들을 새로운 배열로 만들어 복사한다.
TrimExcess() | 사용하지 않은 메모리 공간을 정리한다.

* 예시 코드
```C#
using System;
using System.Collections.Generic;

namespace StackDemo
{
  class Program
  {
    static void Main()
    {
      //새로운 스택의 인스턴스를 생성한다.
      Stack<int> st = new Stack<int>();

      st.Push(11);
      st.Push(22);
      st.Push(33);

      Console.WriteLine(st.Count + "개의 자료가 있습니다.\n");
      Console.Write("맨 위에 있는 값은 " + st.Peek() + "입니다.\n");
      Console.Write("맨 위에 있는 값 " + st.Pop() + "을 삭제합니다.\n");

      Console.WriteLine("\n----------");

      Console.WriteLine(st.Count + "개의 자료가 있습니다.\n");
      Console.Write("맨 위에 있는 값은 " + st.Peek() + "입니다.\n");

      Console.WriteLine("\n----------");

      foreach (int i in st)
      {
        Console.Write(i + " ");
      }

      Console.WriteLine("\n----------");

      st.Push(44);
      st.Push(55);

      Console.WriteLine(st.Count + "개의 자료가 있습니다.\n");
      Console.Write("맨 위에 있는 값은 " + st.Peek() + "입니다.\n");

      Console.WriteLine("\n----------");

      foreach (int i in st)
      {
        Console.Write(i + " ");
      }

      st.TrimExcess(); //사용하지 않는 메모리 공간을 정리한다.

      Console.WriteLine("\n----------");

      if (st.Contains(44))
      {
        st.Clear();
      }

      Console.WriteLine(st.Count + "개의 자료가 있습니다.\n");
    }
  }
}
```
