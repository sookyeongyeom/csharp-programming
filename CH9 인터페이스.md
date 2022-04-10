# C# 프로그래밍 - CH9 인터페이스

## 인터페이스

개발자가 실수하지 않게 도와주는 기능

특별한 기능이 아니라 `이런 최소 사항을 지켜서 만들면 나머지는 우리가 처리해주겠다` 라는 규약임

인터페이스는 모두 대문자 `I` 로 시작함

<br>

## IComparable 인터페이스

비교할 때 사용하는 규약

다음과 같은 모델 클래스가 있다고 가정함

```cs
class Program
{
    class Product
    {
        public string Name { get; set; }
        public int Price { get; set; }

        public override string ToString()
        {
            return Name + " : " + Price + "원";
        }
    }

    static void Main(string[] args)
    {
        List<Product> list = new List<Product>()
        {
            new Product() { Name = "고구마", Price = 1500 },
            new Product() { Name = "사과", Price = 2400 },
            new Product() { Name = "바나나", Price = 1000 },
            new Product() { Name = "배", Price = 3000 }
        };
        list.Sort();    // 오류 발생

        foreach (var item in list)
        {
            Console.WriteLine(item);
        }
    }
}
```

오류가 발생하는 이유 → 해당 클래스를 어떤 기준으로 정렬해야할지 모르기 때문임

이러한 기준을 정해주려면 해당 클래스 내부에 IComparable 인터페이스를 구현해주어야 함

인터페이스를 구현하려면 해당 인터페이스를 클래스 상속하듯 적어주면 됨

```cs
class Product : IComparable
{
    public string Name { get; set; }
    public int Price { get; set; }

    public override string ToString()
    {
        return Name + " : " + Price + "원";
    }
}
```

이후 IComparable 에 커서를 놓고 `Ctrl` + `.` 를 누른 후 `인터페이스 구현` 을 클릭하면 CompareTo() 메서드가 자동으로 생성됨

```cs
class Product : IComparable
{
    public string Name { get; set; }
    public int Price { get; set; }

    public override string ToString()
    {
        return Name + " : " + Price + "원";
    }

    public int CompareTo(object obj)
    {
        throw new NotImplementedException();
    }
}
```

IComparable 인터페이스는 CompareTo() 메서드를 구현해야 한다는 규약을 갖고 있으므로 다음과 같이 Price 속성의 CompareTo() 메서드로 Price 속성끼리 비교할 수 있도록 해줌

```cs
public int CompareTo(object obj)
{
    return this.Price.CompareTo((obj as Product).Price);
}
```

참고로 Price 속성은 int 자료형이며, C# 내부에서 int 자료형은 IComparable 인터페이스의 규약을 지키므로 Price 속성에 CompareTo() 메서드가 있는 것

이제 코드를 실행하면 Sort() 메서드가 정상적으로 실행됨

이렇듯 Sort() 를 실행하려면 반드시 CompareTo() 메서드를 구현해야하며, 실수로 구현하지 않을 시 정렬에서 문제가 발생함

따라서 CompareTo() 메서드를 무조건 구현하게 만드는 IComparable 인터페이스를 사용하도록 하는 것임

<br>

## 인터페이스 인스턴스화

인터페이스는 실체가 없는 규칙이므로 인스턴스화할 수 없음

<br>

## IDisposable 인터페이스

C# 자체에서 제공하는 인터페이스는 메서드를 호출할 때뿐만 아니라, 키워드를 사용할 때에도 적용됨

IDisposable 인터페이스는 using 블록을 사용할 때 자동으로 호출되는 규약임

```cs
class Program
{
    class Dummy : IDisposable
    {

    }

    static void Main(string[] args)
    {

    }
}
```

마찬가지로 IDisposable 에 커서를 놓고 `Ctrl` + `.` 를 누른 후 `인터페이스 구현` 을 클릭하면 Dispose() 메서드가 자동으로 생성됨

```cs
class Program
{
    class Dummy : IDisposable
    {
        public void Dispose()
        {
            throw new NotImplementedException();
        }
    }

    static void Main(string[] args)
    {

    }
}
```

파일 처리와 관련된 내용을 배우지 않았으므로 다음과 같이 간단한 출력만 하도록 Dispose() 메서드를 구현함

```cs
class Program
{
    class Dummy : IDisposable
    {
        public void Dispose()
        {
            Console.WriteLine("Dispose() 메서드를 호출합니다.");
        }
    }

    static void Main(string[] args)
    {
        Dummy dummy = new Dummy();
        dummy.Dispose();
    }
}
```

Dispose() 메서드는 using 블록이라는 기능을 사용할 때 자동으로 호출되는 기능임

따라서 아래와 같이 코드를 구성한 경우, using 블록의 괄호 내에서 생성한 클래스가 IDisposable 인터페이스의 상속을 받을 경우, using 블록을 벗어날 때 자동으로 Dispose() 메서드를 호출함

```cs
static void Main(string[] args)
{
    using (Dummy dummy = new Dummy())
    {

    }
}
```

코드를 실행하면 Dispose() 메서드를 따로 호출하지 않아도 실행되는 것을 볼 수 있음

<br>

## 인터페이스 생성

`interface` `인터페이스 이름` `{ }`

인터페이스는 클래스와 동급의 카테고리로, 클래스를 생성하는 위치라면 어디서든지 만들 수 있음

인터페이스를 생성할 때는 `interface` 키워드를 사용함

같은 파일에 인터페이스를 생성할 시, 클래스를 생성할 때와 같은 위치에 인터페이스를 넣어주면 됨

그러나 인터페이스는 여러 곳에서 사용할 규약이므로 이렇게 한 파일 내부에서 클래스와 같이 생성하는 경우는 없음

마찬가지로 클래스 내부에 인터페이스를 생성하는 경우도 없음

따라서 다른 파일에 생성해주어야 함

다른 파일에 인터페이스를 생성하기 위해서는 클래스를 생성할 때와 마찬가지로,

`프로젝트` > `마우스 오른쪽 버튼` > `추가` > `새 항목` > `인터페이스` 를 선택하면 됨

이렇게 추가한 인터페이스는 다음과 같은 형태로 생성됨

```cs
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;

namespace InterfaceBasic
{
    interface IBasic
    {

    }
}
```

<br>

## 인터페이스 멤버

인터페이스 내부에는 클래스 내부에 넣을 수 있었던 인스턴스 메서드와 속성을 넣을 수 있음

인터페이스 생성

```cs
interface IBasic
{
    int TestInstanceMethod();       // 메서드에 내부 구현을 입력할 수 없음
    int TestProperty { get; set; }      // 속성에도 내부 구현을 입력할 수 없음
}
```

인터페이스 상속

```cs
class Program
{
    class TestClass : IBasic
    {

    }

    static void Main(string[] args)
    {

    }
}
```

인터페이스 구현 (인터페이스에 커서 올린 후 `Ctrl` + `.` > `인터페이스 구현`)

```cs
class TestClass : IBasic
{
    public int TestInstanceMethod()
    {
        throw new NotImplementedException();    // 이후 구현
    }

    public int TestProperty
    {
        get
        {
            throw new NotImplementedException();    // 이후 구현
        }
        set
        {
            throw new NotImplementedException();    // 이후 구현
        }
    }
}
```

<br>

## 인터페이스 다형성

인터페이스를 구현한 클래스는 인터페이스를 상속하게 됨

따라서 다형성을 구현할 수 있게 되므로 다음과 같은 코드가 가능해짐

```cs
static void Main(string[] args)
{
    IBasic basic = new TestClass();     // 클래스가 부모인 인터페이스로 자료형 변환
}
```

<br>

## 인터페이스 다중 상속

인터페이스를 사용하면 다중 상속과 비슷한 기능을 구현할 수 있음

언어의 성능 저하와 디자인상의 이유로 인해 현대 프로그래밍 언어에서는 하나의 클래스는 하나의 클래스만 상속받을 수 있음

그러나 인터페이스를 사용한 다중 상속은 대부분의 현대 프로그래밍 언어에서 허용하고 있음

클래스 상속과 인터페이스 상속을 함께 활용하면 하나의 클래스가 여러 다형성을 가질 수 있게 됨

```cs
class Program
{
    class Parent { }

    class Child : Parent, IDisposable, IComparable      // 한 개의 클래스와 두 개의 인터페이스를 상속받음
    {
        public void Dispose()
        {
            throw new NotImplementedException();    // IDisposable 인터페이스 구현
        }

        public int CompareTo(object obj)
        {
            throw new NotImplementedException();    // IComparable 인터페이스 구현
        }
    }

    static void Main(string[] args)
    {

    }
}
```

이렇게 상속한 경우 다음과 같이 세 종류로 자료형 변환이 가능해짐

```cs
Child child = new Child();
Parent childAsParent = new Child();
IDisposable childAsDisposable = new Child();
IComparable childAsComparable = new Child();
```

인터페이스를 활용하면 코드에 규약을 부여하여 여러 사람이 함께 작업할 때 안정성을 높힐 수 있음

인터페이스를 어떻게 활용하는지 알고 싶다면 디자인 패턴과 관련된 내용을 살펴보면 됨 (디자인 패턴의 90% 이상은 인터페이스를 활용함)

- [Head First Design Pattern](https://www.hanbit.co.kr/store/books/look.php?p_code=B9860513241)

<br>

## 파일 처리 (IDisposable 인터페이스)

파일에 문자열 쓰기

```cs
class Program
{
    static void Main(string[] args)
    {
        File.WriteAllText(@"C:\test\test.txt", "문자열을 파일에 씁니다.");
    }
}
```

문자열 앞에 `@` 기호를 붙여주면 문자열 내부에서 이스케이프 문자를 사용할 수 없는 대신 `\` 기호를 곧바로 문자열로 인식하므로 경로 입력 시 코드의 가독성을 높일 수 있음

파일에 문자열 쓰고 읽기

```cs
class Program
{
    static void Main(string[] args)
    {
        File.WriteAllText(@"C:\test\test.txt", "문자열을 파일에 씁니다.");      // 디렉토리가 존재하지 않으면 오류 발생
        Console.WriteLine(File.ReadAllText(@"C:\test\test.txt"));
    }
}
```

```
문자열을 파일에 씁니다.
```

아주 큰 용량의 파일을 한꺼번에 쓰거나 읽는 것은 시스템에 부담이 가는 일이므로, C#은 파일을 한 줄씩 읽고 쓰는 방법을 굉장히 다양하게 제공함

한 줄씩 쓸 때는 StreamWriter 클래스를 사용함

StreamWriter 클래스를 추가 후에 `F12` 를 눌러 정의로 이동해보면, StreamWriter 클래스는 abstract TextWriter 클래스를 상속받으며, TextWriter 클래스는 IDisposable 의 상속을 받음을 확인할 수 있음

결과적으로 StreamWriter 클래스는 IDisposable 인터페이스를 구현한 클래스임

따라서 using 구문을 사용해 다음과 같이 코드를 구성하는 것이 기본임

```cs
static void Main(string[] args)
{
    using (StreamWriter writer = new StreamWriter())
    {

    }
}
```

이렇게 코드를 구성하면 using 구문을 탈출할 때 자동으로 StreamWriter 클래스의 인스턴스가 가진 Dispose() 메서드를 호출하게 됨

StreamWriter 클래스의 인스턴스는 Write() 또는 WriteLine() 메서드로 다음과 같이 글자를 입력할 수 있음

```cs
static void Main(string[] args)
{
    using (StreamWriter writer = new StreamWriter(@"C:\test\test.txt"))
    {
        writer.WriteLine("안녕하세요");
        writer.WriteLine("StreamWriter 클래스를 사용해");
        writer.WriteLine("글자를 여러 줄 입력해봅니다.");

        for (int i=0; i<10; i++)
        {
            writer.WriteLine("반복문 - " + i);
        }
    }

    Console.WriteLine(File.ReadAllText(@"C:\test\test.txt"));
}
```

한 줄씩 읽을 때는 StreamReader 클래스를 사용함

StreamReader 클래스도 IDisposable 인터페이스를 구현하고 있으므로 using 구문을 사용할 수 있음

```cs
static void Main(string[] args)
{
    using (StreamReader reader = new StreamReader(@"C:\test\test.txt"))
    {
        string line = reader.ReadLine();
        Console.WriteLine(line);
    }
}
```

ReadLine() 메서드는 한 줄 읽으라는 뜻이므로 전체 파일 내용을 읽고 싶을 때는 반복문을 사용해서 읽어줘야 함

```cs
static void Main(string[] args)
{
    using (StreamReader reader = new StreamReader(@"C:\test\test.txt"))
    {
        string line;
        while ((line = reader.ReadLine())!=null)
        {
            Console.WriteLine(line);
        }
    }
}
```
