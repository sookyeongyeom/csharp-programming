# C# 프로그래밍 - CH4 반복문

## 반복문 예시

```cs
for (int i=0; i<1000; i++)
{
    Console.WriteLine(i);
}
```

<br>

## 배열

배열 != 리스트

int[] arr = { 1, 2, 3 };

접근은 인덱스로 가능 arr[0] (단, 음수로 접근 불가)

빈배열 생성 시 int[] arr = new int[100];

이때, 숫자 자료형은 0, 문자열 자료형은 빈 문자열, 객체는 null로 초기화됨

요소 개수 확인 시 Length 속성을 사용 arr.Length

<br>

## while문

```cs
while (true)
{
    Console.WriteLine("무한 반복");
}
```
```cs
int i = 0;
int[] arr = { 10, 12, 15, 19, 21 };

while (i < arr.Length)
{
    Console.WriteLine(i + "번째 출력:" + arr[i]);
    i++;
}
```

<br>

## do while문

조건의 참 거짓 여부와 상관없이 내부의 문장을 최소 한 번은 실행함

```cs
do
{
    Console.WriteLine("무한 반복");
} while (true);
```
```cs
string input;

do
{
    Console.Write("입력(exit을 입력하면 종료): ");
    input = Console.ReadLine();
} while (input != "exit");
```

<br>

## for문

기본

```cs
for (int i=0; i<1000; i++)
{
    Console.WriteLine(i);
}
```

0부터 100까지 더하기

```cs
int sum = 0;

for (int i=1; i<101; i++)
{
    sum += i;
}

Console.WriteLine(sum);
```

1부터 20까지 곱하기

```cs
long mul = 1;

for (int i=1; i<21; i++)
{
    mul *= i;
}

Console.WriteLine(mul);
```

한글 전부 출력하기

```cs
for (char i='가'; i<='힣'; i++)
{
    Console.WriteLine(i);
}
```

<br>

## 역 for문

```cs
int[] arr = { 1, 2, 3, 4, 5, 6 };

for (int i=arr.Length-1; i>=0; i--)
{
    Console.WriteLine(arr[i]);
}
```

<br>

## foreach문

컬렉션에 쉽게 반복문을 적용할 때에 사용함 (ex.배열)

```cs
string[] arr = { "사과", "오렌지", "바나나" };

foreach (string item in arr)
{
    Console.WriteLine(item);
}
```

var 키워드 사용 (더 일반적)

```cs
string[] arr = { "사과", "오렌지", "바나나" };

foreach (var item in arr)
{
    Console.WriteLine(item);
}
```

<br>

## 코드 조각

if, while, for, foreach + `tab` 2회

`tab`으로 키워드 간 이동하여 쉽게 수정 가능

<br>

## 중첩 반복문

별 피라미드

```cs
for (int i=1; i<11; i++)
{
    for (int j=0; j<i; j++)
    {
        Console.Write('*');
    }
    
    Console.WriteLine();
}
```

역 별 피라미드

```cs
for (int i=1; i<11; i++)
{   
    for (int k=0; k<10-i; k++)
    {
        Console.Write(' ');
    }
    for (int j=0; j<i; j++)
    {
        Console.Write('*');
    }

    Console.WriteLine();
}
```

<br>

## break 키워드

```cs
while (true)
{
    Console.Write("숫자를 입력하세요(짝수를 입력하면 종료): ");
    int input = int.Parse(Console.ReadLine());
    if (input % 2 == 0)
    {
        break;
    }
}
```

<br>

## goto 키워드

지정한 레이블로 순간 이동함

goto doNotUse; 이렇게 적으면 doNotUse: 부분으로 코드의 흐름이 즉시 이동한다고 생각하면 됨

사용하지 말 것

<br>

## continue 키워드

홀수만 출력하기 (키워드O)

```cs
for (int i=1; i<10; i++)
{
    if (i%2==0)
    {
        continue;
    }
    Console.WriteLine(i);
}
```

홀수만 출력하기 (키워드X)

```cs
for (int i=1; i<10; i++)
{
    if (i%2!=0)
    {
        Console.WriteLine(i);
    }
}
```

<br>

## 응용예제 - 문자열 처리

C#의 모든 문자열 처리 메서드는 자신을 변경하지 않고 반환함

무슨 소리냐면 input.ToUpper() 을 해도 input 자체는 변경되지 않는다는 뜻임

이런 메서드를 비파괴적 메서드라고 부르기도 함

<br>

## Split()

문자열을 특정한 문자 또는 문자열 기준으로 자르고, 결과를 문자열 배열로 반환함

매개변수로 char 배열을 넣을 수 있음 (여러 개의 문자를 입력하면 여러 문자를 기준으로 자를 수 있음)

```cs
string input = "모찌 정아 포뇨";
string[] inputs = input.Split(new char[] { ' ' });

foreach (var item in inputs)
{
    Console.WriteLine(item);
}
```

여러 개의 문자 기준으로 자르기

```cs
string input = "하얀!모찌 까만!정아 빨간!포뇨";
string[] inputs = input.Split(new char[] { ' ', '!' });

foreach (var item in inputs)
{
    Console.WriteLine(item);
}
```

<br>

## Trim()

문자열 양 옆의 공백을 제거함

```cs
string input = " test      \n";
Console.WriteLine("::" + input.Trim() + "::");
```

TrimStart() = 문자열 앞의 공백 제거 

TrimEnd() = 문자열 뒤의 공백 제거 

<br>

## string.Join()

배열에 있는 요소를 연결해서 문자열로 반환함

```cs
string[] arr = { "포카칩", "에이스", "초코비" };
Console.WriteLine(string.Join(",", arr));
```

<br>

## 이동하는 달팽이

Console.Clear() = 콘솔 화면을 지움

Console.SetCursorPosition() = 콘솔 화면의 특정한 위치로 커서를 옮김

Thread.Sleep() = 스레드 정지

```cs
int x = 1;
while (x<50)
{
    Console.Clear();
    Console.SetCursorPosition(x, 5);

    if (x%3==0)
    {
        Console.WriteLine("__@");
    }
    else if (x%3==1)
    {
        Console.WriteLine("_^@");
    }
    else
    {
        Console.WriteLine("^_@");
    }

    Thread.Sleep(100);
    x++;
}
```

<br>

## 무한 반복하며 이동하기

```cs
bool state = true;
while (state)
{
    ConsoleKeyInfo info = Console.ReadKey();
    switch (info.Key)
    {
        case ConsoleKey.UpArrow:
            Console.WriteLine("위로 이동");
            break;
        case ConsoleKey.RightArrow:
            Console.WriteLine("오른쪽으로 이동");
            break;
        case ConsoleKey.DownArrow:
            Console.WriteLine("아래로 이동");
            break;
        case ConsoleKey.LeftArrow:
            Console.WriteLine("왼쪽으로 이동");
            break;
        case ConsoleKey.X:
            state = false;
            break;
    }
}
```

<br>

## 무한 반복하여 이동하며 글자를 원하는 위치에 출력하기

```cs
int x = 5;
int y = 5;
bool state = true;
while (state)
{
    Console.Clear();
    Console.SetCursorPosition(x, y);
    Console.Write("@");
    ConsoleKeyInfo info = Console.ReadKey();
    switch (info.Key)
    {
        case ConsoleKey.UpArrow:
            y -= 1;
            break;
        case ConsoleKey.RightArrow:
            x += 1;
            break;
        case ConsoleKey.DownArrow:
            y += 1;
            break;
        case ConsoleKey.LeftArrow:
            x -= 1;
            break;
        case ConsoleKey.X:
            state = false;
            break;
    }
}
```
