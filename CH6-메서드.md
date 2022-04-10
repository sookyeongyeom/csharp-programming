# C# 프로그래밍 - CH6 메서드

## 메서드

`접근 제한자` `반환형` `메서드 이름`(`매개변수`)
{
    `메서드 코드`
}

기본

```cs
class Test
{
    public int Power(int x)
    {
        return x * x;
    }
}

static void Main(string[] args)
{
    Test test = new Test();
    Console.WriteLine(test.Power(10));
    Console.WriteLine(test.Power(20));
}
```

두 개의 매개변수를 갖는 메서드

```cs
class Test
{
    public int Multi(int x, int y)
    {
        return x * y;
    }
}

static void Main(string[] args)
{
    Test test = new Test();
    Console.WriteLine(test.Multi(2, 4));
    Console.WriteLine(test.Multi(3, 5));
}
```

메서드는 아무것도 반환하지 않아도 됨

이 경우 `반환형` 위치에 `void` 를 입력할 것

아무것도 반환하지 않는 메서드는 반환이라는 것에 목적을 두기보다, 메서드 내부에서 일어나는 처리에 비중을 둠 (ex.Main())

```cs
class Test
{
    public void Print()
    {
        Console.WriteLine("Print() 메서드가 호출되었습니다.")
    }
}

static void Main(string[] args)
{
    Test test = new Test();
    test.Print();
}
```

<br>

## 매개변수와 반환

min부터 max까지의 숫자를 더해 반환하는 메서드

```cs
class Test
{
    public int Sum(int min, int max)
    {
        int output = 0;
        for (int i=min; i<=max; i++)
        {
            output += i;
        }
        return output;
    }
}

static void Main(string[] args)
{
    Test test = new Test();
    Console.WriteLine(test.Sum(1, 10));
}
```

min부터 max까지의 숫자를 곱해 반환하는 메서드

```cs
class Test
{
    public long Multi(int min, int max)
    {
        long output = 1;
        for (int i=min; i<=max; i++)
        {
            output *= i;
        }
        return output;
    }
}

static void Main(string[] args)
{
    Test test = new Test();
    Console.WriteLine(test.Multi(1, 20));
}
```

<br>

## 클래스 메서드

변수와 마찬가지로, 메서드도 인스턴스 메서드와 클래스 메서드가 있음

클래스 변수와 마찬가지로, 클래스 메서드 생성 시 접근 제한자 뒤에 `static` 키워드를 붙여줌

`접근 제한자` `static` `반환형` `메서드 이름` (`매개변수`) { `메서드 코드` }

인스턴스를 생성하지 않아도 클래스 이름 뒤에 `.` 기호를 찍고 곧바로 사용할 수 있음

```cs
class MyMath
{
    public static int Abs(int input)
    {
        if (input<0)
        {
            return -input;
        }
        else
        {
            return input;
        }
    }
}

static void Main(string[] args)
{
    Console.WriteLine(MyMath.Abs(-15));
    Console.WriteLine(MyMath.Abs(20));
}
```

<br>

## 클래스 메서드에서 사용할 수 없는 것

`static` 키워드를 붙인 변수 또는 메서드는 프로그램을 실행하는 순간에 메모리에 올라가게 됨

클래스 메서드에서는 아직 메모리에 올라가지 않은 인스턴스 변수와 인스턴스 메서드를 사용할 수 없음

즉, 다음과 같은 코드에서는 오류가 발생함

```cs
class Program
{
    public int instanceVar = 10;

    static void Main(string[] args)
    {
        Console.WriteLine(instanceVar);
    }
}
```

이를 수정하려면 사용하고자 하는 인스턴수 변수와 인스턴스 메서드에 `static` 키워드를 붙여 클래스 변수와 클래스 메서드로 만들어주어야 함

```cs
class Program
{
    public static int instanceVar = 10;

    static void Main(string[] args)
    {
        Console.WriteLine(instanceVar);
    }
}
```

<br>

## 오버로딩

(≠ 오버라이딩)

이름은 같고, 매개변수는 다른 메서드를 만드는 것을 오버로딩이라고 부름

```cs
class MyMath
{
    public static int Abs(int input)
    {
        if (input<0) { return -input; }
        else { return input; }
    }

    public static double Abs(double input)
    {
        if (input<0) { return -input; }
        else { return input; }
    }

    public static long Abs(long input)
    {
        if (input<0) { return -input; }
        else { return input; }
    }
}

static void Main(string[] args)
{
    Console.WriteLine(MyMath.Abs(50));
    Console.WriteLine(MyMath.Abs(-50));

    Console.WriteLine(MyMath.Abs(50.123));
    Console.WriteLine(MyMath.Abs(-50.123));

    Console.WriteLine(MyMath.Abs(21474836470));
    Console.WriteLine(MyMath.Abs(-21474836470));
}
```

오버로딩은 이름이 같고 매개변수가 다를 때 일어남

반환값이 다르다고 해서 오버로딩이 일어나지는 않음

즉, 다음과 같은 코드에서는 오류가 발생함

```cs
class Test
{
    public int Test(int input) { }
    public double Test(int input) { }
    public long Test(int input) { }
}
```

메서드를 호출할 때 어떤 메서드를 호출해야하는지 정확히 알 수 없기 때문임

<br>

## 접근 제한자

`접근 제한자` `자료형` `변수 이름`;

`접근 제한자` `반환형` `메서드 이름`(`매개변수`) { `메서드 코드` }

C#은 접근 제한자가 굉장히 많음 (모두 알아보는 것은 불가능)

`private` 과 `public` 이 가장 많이 사용됨

<br>

## private 접근 제한자

접근 제한자를 입력하지 않으면 자동으로 `private` 이 설정됨

Main() 메서드를 보면 접근 제한자가 적혀있지 않으므로 `private` 접근 제한자가 설정되어있다고 볼 수 있음

```cs
static void Main(string[] args)
{

}
```

`private` 접근 제한자가 걸리면 외부 클래스에서 접근할 수 없음

즉, 다음과 같은 코드에서는 오류가 발생함

```cs
class Test
{
    public void TestMethod()
    {
        Program.Main(new string[] { "" });
    }
}

class Program
{
    static void Main(string[] args)
    {

    }
}
```

한편, 자신의 클래스 내부에서는 해당 메서드를 호출할 수 있음

자신의 클래스 내부의 메서드 뿐만 아니라, 자신의 클래스 내부에 있는 클래스의 메서드에서도 접근 가능함

```cs
class Program
{
    class Test
    {
        public void TestMethod()
        {
            Program.Main(new string[] { "" });  // 자신의 클래스 내부 클래스의 메서드
        }
    }

    public void TestMethod()
    {
        Program.Main(new string[] { "" });  // 자신의 클래스 내부의 메서드
    }

    static void Main(string[] args)
    {

    }
}
```

<br>

## public 접근 제한자

외부 클래스에서 Main() 메서드를 호출하고 싶다면, `public` 접근 제한자를 붙여 공개 상태로 만들어주면 됨

```cs
class Test
{
    public void TestMethod()
    {
        Program.Main(new string[] { "" });
    }
}

class Program
{
    public static void Main(string[] args)
    {

    }
}
```

`public` 접근 제한자가 걸린 변수 또는 메서드는 모든 곳에서 접근할 수 있음

외부에서 정말 사용할 일이 없는 변수 또는 메서드는 안전하게 `private` 을 붙여주는 것이 좋음

<br>

## 생성자

무언가를 생성할 때 자동으로 호출되는 메서드

인스턴스 생성자 = 인스턴스를 생성할 때 자동으로 호출되는 메서드

인스턴스 생성자의 조건

1. 이름이 클래스 이름과 같아야 함

2. 접근 제한자는 `public` 이어야 함 (`private` 생성자는 기능이 다름)

3. 반환과 관련된 선언을 하지 않음

생성자는 일반적으로 인스턴스 변수를 초기화하는 일을 함

<br>

## public 생성자

`public` `클래스 이름`(`매개변수`) { }

```cs
class Product
{
    public string name;
    public int price;

    public Product(string name, int price)
    {
        this.name = name;
        this.price = price;
    }
}
```

인스턴스 생성 시 카운터 증가 & 생성된 순서를 자신의 id로 지정

```cs
class Program
{
    class Product
    {
        public static int counter = 0;
        public int id;
        public string name;
        public int price;

        public Product(string name, int price)
        {
            Product.counter = counter + 1;
            this.id = counter;
            this.name = name;
            this.price = price;
        }
    }

    static void Main(string[] args)
    {
        Product productA = new Product("감자", 1000);
        Product productB = new Product("고구마", 1500);
        Product productC = new Product("당근", 2000);

        Console.WriteLine(productA.id + " : " + productA.name);
        Console.WriteLine(productB.id + " : " + productB.name);
        Console.WriteLine(productC.id + " : " + productC.name);

        Console.WriteLine("총 개수 : " + Product.counter + "개");
    }
}
```

<br>

## private 생성자

생성자로 클래스의 인스턴스를 만들 수 없게 하고 싶을 때 `private` 생성자를 사용함

즉, 다음과 같은 코드에서는 오류가 발생함

```cs
class Program
{
    class Hidden
    {
        private Hidden() { }
    }

    static void Main(string[] args)
    {
        Hidden hidden = new Hidden();
    }
}
```

이런 기능이 왜 필요할까?

1. 클래스가 정적 멤버만 갖고 있을 때 (변하지 않는 멤버)

2. 팩토리 메서드 패턴에서 팩토리 메서드로만 인스턴스를 생성하게 하고 싶을 때

<br>

## static 생성자 (=정적 생성자)

정적 요소를 초기화할 때 사용되는 생성자

```cs
class Sample
{
    public static int value;

    static Sample()
    {
        value = 10;
        Console.WriteLine("정적 생성자 호출");
    }
}
```

정적 생성자를 만들 때는 제한이 있음

1. 접근 제한자를 사용하지 못함

2. 매개변수를 사용하지 못함

정적 생성자는 정적 요소를 사용할 때, 또는 인스턴스를 생성하는 초기 시점에 한 번만 호출됨 (해당 클래스와 관련된 요소를 처음 사용하는 시점에 자동적으로 호출되며, 별도로 호출 불가능)

```cs
static void Main(string[] args)
{
    Console.WriteLine("안녕!");
    Console.WriteLine(Sample.value);    // 이 때 한 번만 호출됨!
    Console.WriteLine("반가워!");
    Sample sample = new Sample();
    Console.WriteLine("잘 부탁해!");
}
```

```cs
static void Main(string[] args)
{
    Console.WriteLine("안녕!");
    Sample sample = new Sample();   // 이 때 한 번만 호출됨!
    Console.WriteLine("반가워!");
    Console.WriteLine(Sample.value);
    Console.WriteLine("잘 부탁해!");
}
```

<br>

## 소멸자

생성자와 반대로 인스턴스가 소멸될 때 호출됨

C#은 변수가 더 이상 사용되지 않을 것이 확실할 때 (주로 가비지 컬렉터가) 객체를 소멸시키며 소멸자를 호출함

`~``클래스 이름`() { }

소멸자를 만들 때는 지켜야 할 규칙이 있음

1. 이름은 클래스 이름 앞에 `~` 기호가 붙은 것이어야 함

2. 접근 제한자를 사용하지 않음

3. 반환과 관련된 선언을 하지 않음

4. 매개변수과 관련된 선언을 하지 않음

5. 하나의 클래스에는 하나의 소멸자만 있을 수 있음

```cs
class Program
{
    class Product
    {
        public string name;
        public int price;

        public Product(string name, int price)
        {
            this.name = name;
            this.price = price;
        }

        ~Product()
        {
            Console.WriteLine(this.name + "의 소멸자 호출");
        }
    }

    static void Main(string[] args)
    {
        Product product = new Product("과자", 1500);
    }
}
```

<br>

## 상수

상수로 선언된 변수는 값을 변경할 수 없음

값을 변경할 필요가 없거나, 값을 변경하는 것이 위험할 때 상수를 사용함

상수를 생성하고 싶다면 변수 또는 속성 앞에 `const` 키워드를 붙여주면 됨

```cs
class MyMath
{
    public const double PI = 3.141592;
}
```

`const` 키워드는 일반적인 메서드 내부에도 사용할 수 있음 (그런 경우가 많지는 않음)

<br>

## readonly 키워드

읽기 전용 키워드 (상수와 크게 다를 바 없음)

클래스 변수 또는 변수 앞에 `readonly` 키워드를 붙여서 생성함

```cs
class Product
{
    private static int count;
    public readonly int id;
    public string name;
    public int price;

    public Product(string name, int price)
    {
        id = count++;   // 생성자에서는 readonly 변수를 변경할 수 있음
        this.name = name;
        this.price = price;
    }
}
```

`readonly` 변수는 변수를 선언하는 시점과 생성자 메서드에서만 값을 변경할 수 있음

<br>

## 캡슐화

인스턴스 생성 시 검증

```cs
class Box
{
    private int width;
    private int height;

    // 생성자
    public Box(int width, int height)
    {
        if (width>0 || height>0)
        {
            this.width = width;
            this.height = height;
        }
        else { Console.WriteLine("너비와 높이는 자연수로 초기화해주세요!"); }
    }

    // 인스턴스 메서드
    public int Area()
    {
        return this.width * this.height;
    }
}
```

문제 → 한 번 생성한 width와 height 변경 불가, 어떤 값이 들어있는지도 확인 불가

해결책 → 겟터와 셋터

<br>

## 겟터와 셋터

변수를 바로 건드릴 수는 없지만 변수를 변경하는 메서드 호출을 통해 변경 가능

```cs
class Box
{
    private int width;
    private int height;

    // 생성자
    public Box(int width, int height)
    {
        if (width>0 || height>0)
        {
            this.width = width;
            this.height = height;
        }
        else { Console.WriteLine("너비와 높이는 자연수로 초기화해주세요!"); }
    }

    // 인스턴스 메서드
    public int Area() { return this.width * this.height; }

    // 겟터(Getter)
    public int GetWidth() { return width; }
    public int GetHeight() { return height; }
    
    // 셋터(Setter)
    public void SetWidth(int width)
    {
        if (width>0) { this.width = width; }
        else { Console.WriteLine("너비는 자연수를 입력해주세요"); }
    }

    public void SetHeight(int width)
    {
        if (height>0) { this.height = height; }
        else { Console.WriteLine("높이는 자연수를 입력해주세요"); }
    }
}
```

문제 → 코드가 너무 길어짐

해결책 → 속성

<br>

## 속성

겟터와 셋터를 손쉽게 만들 수 있는 방법

생성 방법이 굉장히 다양하지만, 일반적으로는 아래와 같음

```cs
private int 변수;

public int 속성
{
    get { return 변수; }
    set { 변수 = value; }
}
```

다음과 같이 사용함

`인스턴스`.`속성`   // 겟터 호출

`인스턴스`.`속성` = `값`    // 셋터 호출

`SetWidth(int width)` 의 매개변수와 같은 기능을 하는 것이 `value` 키워드임

<br>

## 일반적인 속성

```cs
class Program
{
    class Box
    {
        // 변수와 속성
        private int width;
        public int Width
        {
            get { return width; }
            set
            {
                if (value>0) { width = value; }
                else { Console.WriteLine("너비는 자연수를 입력해주세요"); }
            }
        }

        private int height;
        public int Height
        {
            get { return height; }
            set
            {
                if (value>0) { height = value; }
                else { Console.WriteLine("높이는 자연수를 입력해주세요"); }
            }
        }

        // 생성자
        public Box(int width, int height)
        {
            Width = width;
            Height = height;
        }

        // 인스턴스 메서드
        public int Area() { return this.width * this.height; }
    }

    static void Main(string[] args)
    {
        Box box = new Box(-10, -20);

        box.Width = -200;
        box.Height = -100;
    }
}
```

<br>

## 간단한 속성 생성 방법

```cs
public int Width { get; set; }
public int Height { get; set; }
```

<br>

## 속성 코드 조각

`prop` + `tab` 2회

```cs
public int MyProperty { get; set; }
```

`propfull` + `tab` 2회

```cs
private int MyVar;

public int MyProperty
{
    get { return myVar; }
    set { myVar = value; }
}
```

<br>

## 재귀 메서드

메서드 내부에서 자기 자신을 호출하는 메서드를 말함

```cs
class Program
{
    static void Main(string[] args)
    {
        Main(new string[0]);
    }
}
```

<br>

## 피보나치 수열

재귀 메서드를 사용한 피보나치 인스턴스 메서드

```cs
class Fibonacci
{
    public long Get(int i)
    {
        if (i<0) { return 0; }
        if (i==1) { return 1; }
        return Get(i-2) + Get(i-1);
    }
}

class Program
{
    static void Main(string[] args)
    {
        Fibonacci fibo = new Fibonacci();
        Console.WriteLine(fibo.Get(1));
        Console.WriteLine(fibo.Get(2));
        Console.WriteLine(fibo.Get(3));
        Console.WriteLine(fibo.Get(4));
        Console.WriteLine(fibo.Get(5));
    }
}
```

재귀 메서드를 사용한 피보나치 클래스 메서드

```cs
class Fibonacci
{
    public static long Get(int i)
    {
        if (i<0) { return 0; }
        if (i==1) { return 1; }
        return Get(i-2) + Get(i-1);
    }
}

class Program
{
    static void Main(string[] args)
    {
        Console.WriteLine(Fibonacci.Get(1));
        Console.WriteLine(Fibonacci.Get(2));
        Console.WriteLine(Fibonacci.Get(3));
        Console.WriteLine(Fibonacci.Get(4));
        Console.WriteLine(Fibonacci.Get(5));
    }
}
```

<br>

## 메모화

한 번 계산했던 값을 저장해두는 기술

```cs
class Fibonacci
{
    private static Dictionary<int, long> memo = new Dictionary<int, long>();

    public static long Get(int i)
    {
        if (i<0) { return 0; }
        if (i==1) { return 1; }

        if (memo.ContainsKey(i)) { return memo[i]; }
        else
        {
            long value = Get(i-2) + Get(i-1);
            memo[i] = value;
            return value;
        }
    }
}

class Program
{
    static void Main(string[] args)
    {
        Console.WriteLine(Fibonacci.Get(40));
        Console.WriteLine(Fibonacci.Get(100));
    }
}
```

`memo` 를 `static` 으로 선언하는 이유 → 클래스 메서드에서는 아직 메모리에 올라가지 않은 인스턴스 변수와 인스턴스 메서드를 사용할 수 없기 때문임
