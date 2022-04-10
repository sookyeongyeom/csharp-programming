# C# 프로그래밍 - CH8 클래스 심화

## 제네릭

```cs
List<int> list = new List<int>();
```

클래스 내부에서 자료형에 별칭(Alias)을 지정하는 기능

```cs
class Wanted<T>
{

}
```

이렇게 `< >` 기호 내부에 식별자를 지정해서 `Wanted<int>` 처럼 사용하면 `T` 에 `int` 자료형이 할당됨

마찬가지로 `Wanted<float>` 처럼 사용하면 `T` 에 `float` 자료형이 할당됨

다음 코드는 제네릭을 사용하여 변수 Value 의 자료형을 원하는 자료형으로 지정함

```cs
class Wanted<T>
{
    public T Value;
    public Wanted(T value)
    {
        this.Value = value;
    }
}

class Program
{
    static void Main(string[] args)
    {
        Wanted<string> wantedString = new Wanted<string>("String");
        Wanted<int> wantedInt = new Wanted<int>(52273);
        Wanted<double> wantedDouble = new Wanted<double>(52.273);

        Console.WriteLine(wantedString.Value);
        Console.WriteLine(wantedInt.Value);
        Console.WriteLine(wantedDouble.Value);
    }
}
```

제네릭을 하나 지정할 때는 보통 식별자로 `T` 를 사용함

두 개 이상의 제네릭을 사용한다면?

```cs
class Test<T, U>
{

}
```

<br>

## where 키워드

제네릭에 모든 자료형을 허용하면 안 되는 경우, `where` 키워드를 사용해서 제네릭을 제한할 수 있음

```cs
class Test<T, U>
    where T : class
    where U : struct
{

}
```

```cs
class Test<T, U>
    where T : IComparable
    where U : IComparable, IDisposable
{

}
```

<br>

## 인덱서

인덱서 선언

```cs
class Products
{
    public int this[int i]
    {
        get { return i; }
        set { Console.WriteLine(i + "번째 상품 설정"); }
    }
}
```

인덱서를 활용하여 배열처럼 사용하는 제곱 클래스

```cs
class SquareCalculator
{
    public int this[int i]
    {
        get { return i * i; }
    }
}

class Program
{
    static void Main(string[] args)
    {
        SquareCalculator square = new SquareCalculator();
        Console.WriteLine(square[10]);
        Console.WriteLine(square[20]);
        Console.WriteLine(square[30]);
    }
}
```

그냥 메서드로 만들어서 사용해도 똑같음

하지만 만약 배열과 유사한 클래스를 만든다면, 인덱서를 활용하여 기존의 배열과 비슷한 방법으로 사용할 수 있게 만드는 것이 편리함

<br>

## out 키워드

값을 여러 개 반환하기 위한 키워드

`out` 키워드를 사용하는 대표적인 메서드는 TryParse() 메서드임

TryParse() 메서드는 파싱 성패 여부와 파싱한 결과값을 동시에 반환함

```cs
class Program
{
    static void Main(string[] args)
    {
        Console.Write("숫자 입력: ");
        int output;
        bool result = int.TryParse(Console.ReadLine(), out output);     // out 키워드를 붙여서 매개변수 넣어주기

        if (result)
        {
            Console.WriteLine("입력한 숫자: " + output);
        }
        else
        {
            Console.WriteLine("숫자를 입력해주세요!");
        }
    }
}
```

위 예시에서, result 에는 파싱 성패 여부가 담기고 output 에는 파싱한 결과값이 담김

<br>

## out 키워드를 사용하는 메서드 생성

```cs
class Program
{
    static void NextPosition(int x, int y, int vx, int vy, out int rx, out int ry)
    {
        // 다음 위치 = 현재 위치 + 현재 속도
        rx = x + vx;
        ry = y + vy;
    }

    static void Main(string[] args)
    {
        int x = 0;
        int y = 0;
        int vx = 1;
        int vy = 1;

        Console.WriteLine("현재 좌표: (" + x + "," + y + ")");
        NextPosition(x, y, vx, vy, out x, out y);   // out 키워드를 붙여서 매개변수 넣어주기
        Console.WriteLine("다음 좌표: (" + x + "," + y + ")");
    }
}
```

<br>

## 구조체

간단한 객체를 만들 때 사용하는 형식

클래스와 거의 동일한 구문을 사용하지만, 복사 형식이 다르고 클래스보다 제한이 조금 많음

또한 상속이 불가능하며, 인터페이스를 구현할 수도 없음

대신 클래스보다 안정성 측면에서는 높음

C#의 기본 자료형은 모두 구조체로 정의되어 있음

<br>

## 구조체 선언

```cs
struct Point
{
    public int x;
    public int y;
}
```

구조체는 `new` 키워드를 사용하지 않아도 인스턴스를 생성할 수 있음

다만 이 경우, 멤버 변수를 별도로 초기화하지 않으면 해당 멤버 변수를 사용할 때 오류가 발생함

<br>

## new 키워드를 사용하지 않고 구조체 인스턴스 생성

```cs
class Program
{
    struct Point
    {
        public int x;
        public int y;
    }

    static void Main(string[] args)
    {
        Point point;
        point.x = 10;
        point.y = 10;

        Console.WriteLine(point.x);
        Console.WriteLine(point.y);
    }
}
```

<br>

## 구조체의 생성자

구조체는 클래스와 다르게, 매개변수 없는 생성자를 선언할 수 없음

따라서 반드시 다음과 같이 매개변수를 넣어 생성자를 만들어야 함

```cs
struct Point
{
    public int x;
    public int y;

    public Point(int x, int y)
    {
        this.x = x;
        this.y = y;
    }
}
```

왜 구조체는 매개변수 없는 생성자를 만들 수 없을까?

이유는 매개변수 없는 생성자가 자동으로 정의되기 때문임

위와 같이 매개변수 있는 생성자를 만들어도, 매개변수 없는 생성자를 사용할 수 있음

이 경우 내부 변수는 해당 자료형의 기본 값으로 초기화됨

숫자 관련 자료형이라면 `0` 으로, 문자열 또는 객체라면 `null` 로 초기화됨

```cs
Point point = new Point();

Console.WriteLine(point.x);
Console.WriteLine(point.y);
```

```
0
0
```

<br>

## 구조체 생성자가 갖는 제약

구조체 생성자에서는 반드시 모든 멤버 변수를 초기화된 상태로 만들어주어야 함

또한 선언과 동시에 멤버 변수를 초기화할 수 없음

```cs
struct Point
{
    public int x;
    public int y;
    public string testA;
    public string testB = "init";   // 선언과 동시에 초기화할 수 없으므로 오류 발생

    public Point(int x, int y)      // 멤버 변수 testA를 초기화하지 않았으므로 오류 발생
    {
        this.x = x;
        this.y = y;
    }
}
```

```cs
struct Point
{
    public int x;
    public int y;
    public string testA;
    public string testB;

    public Point(int x, int y)      // 생성자 오버로딩
    {
        this.x = x;
        this.y = y;
        this.testA = "초기화";
        this.testB = "초기화";
    }

    public Point(int x, int y, string test)     // 생성자 오버로딩
    {
        this.x = x;
        this.y = y;
        this.testA = test;
        this.testB = test;
    }
}
```

이렇듯 복잡한 이유는 구조체의 가장 중요한 의미가 안정성이기 때문임

따라서 모든 매개변수를 초기화해서 사용하게 만드는 것

<br>

## 구조체 복사

구조체는 값 복사가 이루어짐

```cs
class Program
{
    class PointClass
    {
        public int x;
        public int y;

        public PointClass(int x, int y)
        {
            this.x = x;
            this.y = y;
        }
    }

    struct PointStruct
    {
        public int x;
        public int y;

        public PointStruct(int x, int y)
        {
            this.x = x;
            this.y = y;
        }
    }

    static void Main(string[] args)
    {
        // 클래스
        PointClass pointClassA = new PointClass(10, 20);
        PointClass pointClassB = pointClassA;   // 참조 복사 발생

        pointClassB.x = 100;
        pointClassB.y = 200;

        Console.WriteLine("pointClassA: " + pointClassA.x + "," + pointClassA.y);
        Console.WriteLine("pointClassB: " + pointClassB.x + "," + pointClassB.y);
        Console.WriteLine();

        // 구조체
        PointStruct pointStructA = new PointStruct(10, 20);
        PointStruct pointStructB = pointStructA;    // 값 복사 발생

        pointStructB.x = 100;
        pointStructB.y = 200;

        Console.WriteLine("pointStructA: " + pointStructA.x + "," + pointStructA.y);
        Console.WriteLine("pointStructB: " + pointStructB.x + "," + pointStructB.y);
    }
}
```

```
pointClassA: 100,200
pointClassB: 100,200

pointStructA: 10,20
pointStructB: 100,200
```
