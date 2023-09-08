# Params 키워드

* 사용자로부터 몇 개의 인수가 전달되는지 미리 정할 수 없는 경우에 사용하는 것이 **params 키워드**
* 인수의 개수를 미리 정하고 있지 않기 때문에 **가변인자**라 부르기도 함
* 예시 코드
```C#
static int TotalSum(params int[] myArray)
{
  int sum = 0;

  for(int i = 0; i < myArray.Length; i++)
  {
    sum += myArray[i];
  }

  return sum;
}

static void Main()
{
  //TotalSum() 함수에 전달되는 인수의 수가 서로 다른 점에 주목
  Console.WriteLine("Sum(1) = {0}", TotalSum(0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10));
  Console.WriteLine("Sum(2) = {0}", TotalSum(1, 3, 5, 7, 9));
}
```
* TotalSum 함수에 전달하는 인수가 서로 다르다는 점 주목!
* But, 함수를 선언할 때 `params` 키워드를 사용했기 때문에 문제가 되지 않음
* params 키워드는 오직 **1차원 배열에서만 사용**할 수 잇음
