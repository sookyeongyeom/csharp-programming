# C# 프로그래밍 - CH5 클래스

## 클래스

클래스 = 사용자 정의 자료형

```cs
class Car
{
    int carNumber;
    DateTime inTime;
    DateTime outTime;

    public void SetInTime()
    {
        this.inTime = DateTime.Now;
    }

    public void SetOutTime()
    {
        this.outTime = DateTime.Now;
    }
}

static void Main(string[] args)
{
    Car car = new Car();
    car.SetInTime();
    car.SetOutTime();
}
```

<br>

## 클래스와 인스턴스

`클래스` `인스턴스` = `new` `생성자`;

Car car = new Car();

클래스를 변수로 선언한 것을 인스턴스 또는 객체라고 부름

또, 클래스 이름과 같은 메서드를 생성자라고 부름

<br>

## 클래스 사용

이미 만들어져 있는 클래스들이 있음 (ex.Random,List,Math)

<br>

## Random 클래스

Next() = 임의의 정수를 생성할 때 사용함

```cs
Random random = new Random();
Console.WriteLine(random.Next(10, 100));
Console.WriteLine(random.Next(10, 100));
Console.WriteLine(random.Next(10, 100));
```

NextDouble() = 0.0~1.0 사이의 난수를 반환함

```cs
Random random = new Random();
Console.WriteLine(random.NextDouble());
Console.WriteLine(random.NextDouble());
Console.WriteLine(random.NextDouble());
```

원하는 범위의 실수 난수 생성 (0.0~10.0)

```cs
Random random = new Random();
Console.WriteLine(random.NextDouble()*10);
Console.WriteLine(random.NextDouble()*10);
Console.WriteLine(random.NextDouble()*10);
```

<br>

## 인스턴스 멤버

위에서와 같이 인스턴스 뒤에 점을 찍고 사용하는 멤버를 인스턴스 멤버라고 부름

해당 멤버가 변수면 인스턴스 변수, 메서드면 인스턴스 메서드, 속성이면 인스턴스 속성 등으로 부름

<br>

## List 클래스

크기가 고정되어 있는 배열과 달리 List 클래스를 사용하면 가변적인 배열을 만들 수 있음

List 클래스는 어떤 자료형의 리스트로 선언하는데, 이때 어떤 자료형인지를 알려주기 위해 Generic을 사용함

<br>

## Generic

클래스 이름 뒤에 `<` 와 `>` 로 감싸 적용함

```cs
List<int> list = new List<int>();
```

<br>

## 클래스 참조 추가

`Ctrl`+`.` 를 눌러 참조를 추가할 수 있음

<br>

## List 요소 추가

Add()

```cs
List<int> list = new List<int>();

list.Add(1);
list.Add(2);
list.Add(3);

foreach (var item in list)
{
    Console.WriteLine("Total Count: " + list.Count + "\tItem: " + item);
}
```

<br>

## List 인스턴스 생성과 동시에 요소 추가

```cs
List<int> list = new List<int>() { 10, 20, 30 };

foreach (var item in list)
{
    Console.WriteLine("Total Count: " + list.Count + "\tItem: " + item);
}
```

<br>

## List 요소 제거

Remove() = 하나만 제거

```cs
List<int> list = new List<int>() { 11, 22, 33 };

list.Remove(22);

foreach (var item in list)
{
    Console.WriteLine("Total Count: " + list.Count + "\tItem: " + item);
}
```

<br>

## Math 클래스

인스턴스를 만들지 않고 사용함

클래스 이름 뒤에 `.` 기호를 찍고 곧바로 멤버 사용

```cs
Console.WriteLine(Math.Abs(-123));
```

Abs(숫자) = 절댓값
Ceiling(숫자) = 크거나 같은 최소 정수 (천장)
Floor(숫자) = 작거나 같은 최대 정수 (바닥)
Max(숫자, 숫자) = 둘 중 큰 수
Min(숫자, 숫자) = 둘 중 작은 수
Round(숫자) = 반올림

<br>

## 클래스 멤버

(↔ 인스턴스 멤버)

Math 클래스처럼 클래스 이름 뒤에 점을 찍고 바로 사용하는 멤버를 클래스 멤버라고 부름

해당 멤버가 변수면 클래스 변수, 메서드면 클래스 메서드, 속성이면 클래스 속성 등으로 부름

<br>

## 클래스 생성

```cs
using System;

namespace ClassBasic
{
    class FirstClass
    {

    }

    class SecondClass
    {

    }

    class Program
    {
        static void Main(string[] args)
        {
        }
    }
}
```

<br>

## 클래스 내부에 클래스 생성

```cs
using System;

namespace ClassBasic
{
    class Program
    {
        class FirstClass
        {

        }

        class SecondClass
        {   

        }
        
        static void Main(string[] args)
        {
        }
    }
}
```

<br>

## 서로 다른 파일에 클래스 생성

클래스를 구현하다보면 길이가 어마어마해지기 때문에 파일 하나에 클래스를 넣고, 파일의 이름과 맞추어 만드는 것이 일반적임

(파일의 이름과 클래스 이름이 다르다고 문제가 발생하지는 않음)

기본

1. 콘솔 이름 우클릭

2. 추가 > 새 항목

3. 클래스 > 원하는 클래스 이름 입력

빠른 생성

1. 일단 Main() 메서드에 새로운 클래스 인스턴스 초기화 (Product product = new Product();)

2. 오류가 발생하면 `Ctrl`+`.` > `Product` 형식 생성 > 새 파일에서 class `Product` 생성

namespace 간 클래스 이름이 충돌되지 않도록 특별한 목적이 없는 한 기존에 존재하는 클래스 이름과 다르게 선언할 것

<br>

## 인스턴스 변수

`접근 제한자` `자료형` `이름`;

```cs
class User
{
    public string name;
    public string password;
    public string address;
}
```

인스턴스 변수는 대부분 private 으로 선언하지만 지금은 접근 제한자를 배우지 않았으므로 일단 public 으로 선언함

<br>

## 인스턴스 변수 생성과 사용

인스턴스 변수 생성

```cs
class Program
{
    class Product
    {
        public string name;
        public int price;
    }

    static void Main(string[] args)
    {
        Product product = new Product();
    }
}
```

인스턴스 변수 사용

```cs
static void Main(string[] args)
{
    Product product = new Product();

    product.name = "감자";
    product.price = 2000;

    Console.WriteLine(product.name + " : " + product.price + "원");
}

인스턴스 변수 생성 시 초기화

```cs
class Product
{
    public string name = "default";
    public int price = 1000;
}
```

인스턴스 생성 시 원하는 변수를 원하는 값으로 초기화 (일반적인 현대 프로그래밍 언어는 지원하지 않는 기능)

```cs
class Product
{
    public string name;
    public int price;
}

static void Main(string[] args)
{
    Product productA = new Product() { name="감자", price=2000 };
    Product productB = new Product() { name="고구마", price=3000 };
}
```

<br>

## 클래스 변수

Math 클래스와 같이 클래스 이름으로 곧바로 사용하는 변수와 메서드를 클래스 변수와 클래스 메서드라고 부름

클래스 변수를 만들 때는 `static` 키워드를 사용함

`접근 제한자` `static` `자료형` `이름`;

```cs
class MyMath
{
    public static double PI = 3.141592;
}

static void Main(string[] args)
{
    Console.WriteLine(MyMath.PI);
}
```

<br>

## 클래스를 사용하는 이유

일반적으로 클래스 기반의 객체 지향 프로그래밍 언어는 다음 네가지의 특징을 갖고 있음

그리고 이 특징이 클래스를 사용하는 기본 이유임

1. 추상화

2. 캡슐화

3. 상속

4. 다형성

<br>

## 추상화

프로그램에 사용되는 핵심적인 부분을 현실로부터 추출하는 것

학생 = 학번, 이름, 학과 등

```cs
class Student
{
    public string id;
    public string name;
    public string major;
}
```

<br>

## 모델 클래스

모델 클래스 = 변수만 갖고 있는 클래스

실제 응용 프로그램 개발을 할 때 만들게 될 클래스의 90%가 이러한 모델 클래스임

```cs
class Student
{
    public string id;
    public string name;
    public int grade;
    public string major;
    public DateTime birthday;
}
```

<br>

## 모델 클래스와 List 클래스

Student 클래스를 리스트(List 클래스의 인스턴스)에 저장하고 출력

```cs
class Student
{
    public string name;
    public int grade;
}

static void Main(String[] args)
{
    List<Student> list = new List<Student>();
    list.Add(new Student() { name="염수경", grade=1 });
    list.Add(new Student() { name="염수연", grade=2 });
    list.Add(new Student() { name="염모찌", grade=3 });

    foreach (var item in list)
    {
        Console.WriteLine(item.name + " : " + item.grade);
    }
}
```

리스트 생성 시 모델 클래스 동시 초기화

```cs
List<Student> list = new List<Student>()
{
    new Student() { name="염수경", grade=1 },
    new Student() { name="염수연", grade=2 },
    new Student() { name="염정아", grade=3 }
};
```

<br>

## List 클래스 요소 제거와 역 반복문

Remove(object element) = 객체를 지정하여 제거
RemoveAt(int index) = 특정 인덱스를 지정하여 제거

foreach 반복문 내부에서는 반복되고 있는 리스트에 추가 또는 제거가 불가능함

즉, foreach 반복문을 사용해서는 요소 제거를 할 수 없음

따라서 아래와 같은 코드에서는 오류가 발생함

```cs
class Student
{
    public string name;
    public int grade;
}

static void Main(string[] args)
{
    List<Student> list = new List<Student>();
    list.Add(new Student() { name="피카츄", grade=1 });
    list.Add(new Student() { name="꼬부기", grade=2 });
    list.Add(new Student() { name="파이리", grade=3 });

    foreach (var item in list)
    {
        if (item.grade > 1)
        {
            list.Remove(item);
        }
    }

    foreach (var item in list)
    {
        Console.WriteLine(item.name + " : " + item.grade);
    }
}
```

아래와 같이 for 반복문을 사용한다면?

```cs
for (int i=0; i<list.Count; i++)
{
    if (list[i].grade > 1)
    {
        list.RemoveAt(i);
    }
}
```

원하는 대로 되지 않음 → 요소가 지워지면서 인덱스가 앞으로 밀리기 때문

따라서 하나 남은 역 for 반복문을 사용해야 함

뒤에서부터 제거하면 다음 검사 대상인 인덱스가 앞으로 밀리는 일이 발생하지 않기 때문

```cs
for (int i = list.Count-1; i>=0; i--)
{
    if (list[i].grade > 1)
    {
        list.RemoveAt(i);
    }
}
```

리스트의 요소를 제거할 때는 반드시 역 for 반복문을 사용해야 함

<br>

## partial 키워드

partial 키워드를 사용하면 클래스를 분할하여 정의할 수 있음 (아예 다른 파일에서도 가능)

```cs
partial class Example
{
    public int a;
}

partial class Example
{
    public int b;
}
```
