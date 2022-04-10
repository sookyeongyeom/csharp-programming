# C# 프로그래밍 - CH12 Linq

## Linq

Linq(Language-Integrated Query)는 컬렉션 형태의 데이터를 쉽게 다루고자 SQL을 본따 만든 구문임

Linq를 사용하면 C# 객체의 집합을 쉽게 관리할 수 있으며, SQL 서버를 연동하여 데이터베이스 관리를 간단하게 할 수도 있음

데이터를 선별하는 정형화된 코드 (Linq X)

```cs
List<int> input = new List<int>() { 1, 2, 3, 4, 5 };
List<int> output = new List<int>();

foreach (var item in input)
{
    if (item%2==0)
    {
        output.Add(item);
    }
}

return output;
```

Linq를 사용하여 위 예제를 간단하게 작성

```cs
List<int> input = new List<int>() { 1, 2, 3, 4, 5 };

return from item in input
        where item%2==0
        select item;
```

<br>

## Linq 기본 구문

Linq 구문은 다음과 같이 이루어져 있음

1. from

2. in

3. where

4. orderby

5. select

```cs
List<int> input = new List<int>() { 1, 2, 3, 4, 5 };
var output = from item in input
                    where item%2==0
                    orderby item
                    select item;
```

그룹화와 조인 등 추가 구문들이 있지만 이 책에서는 다루지 않음

<br>

## from in select 구문

모든 Linq 쿼리는 from, in, select 키워드를 포함해야 함

```cs
from <변수 이름(원하는 이름 지정)> in <컬렉션 이름>
select <결과에 넣을 요소>
```

```cs
List<int> output = new List<int>();
foreach (var <변수 이름(원하는 이름 지정)> in <컬렉션 이름>)
{
    output.Add(<결과에 넣을 요소>);
}
```

기존의 리스트에서 요소를 제곱한 새로운 요소를 가진 리스트를 생성하는 예제

```cs
static void Main(string[] args)
{
    List<int> input = new List<int>() { 1, 2, 3, 4, 5 };

    var output = from item in input
                select item * item;

    foreach (var item in output)
    {
        Console.WriteLine(item);
    }
}
```

```
1
4
9
16
25
```

<br>

## where 구문

조건을 지정할 때 사용함

```cs
from <변수 이름(원하는 이름 지정)> in <컬렉션 이름>
where <조건식>
select <변수 이름(원하는 이름 지정)>
```

```cs
List<int> output = new List<int>();
foreach (var <변수 이름(원하는 이름 지정)> in <컬렉션 이름>)
{
    if (조건식)
    {
        output.Add(<결과에 넣을 요소>);
    }
}
```

리스트에서 요소가 5 초과, 짝수인 것만을 뽑아 새로운 리스트를 생성하는 예제

```cs
static void Main(string[] args)
{
    List<int> input = new List<int>() { 1, 2, 3, 4, 5, 6, 7, 8, 9, 10 };

    var output = from item in input
                    where (item>5) && (item%2==0)
                    select item;

    foreach (var item in output)
    {
        Console.WriteLine(item);
    }
}
```

<br>

## orderby 구문

ascending = 오름차순 (기본)

descending = 내림차순

```cs
from <변수 이름(원하는 이름 지정)> in <컬렉션 이름>
where <조건식>
orderby <정렬 대상> <정렬 순서>
select <변수 이름(원하는 이름 지정)>
```

요소를 내림차순 정렬한 새로운 리스트를 생성하는 예제

```cs
static void Main(string[] args)
{
    List<int> input = new List<int>() { 1, 2, 3, 4, 5, 6, 7, 8, 9, 10 };

    var output = from item in input
                    where (item>5) && (item%2==0)
                    orderby item descending
                    select item;

    foreach (var item in output)
    {
        Console.WriteLine(item);
    }
}
```

<br>

## Linq 결과의 자료형과 반환

IEnumerable 인터페이스의 다형성을 활용하여 다음과 같이 자료형을 지정하고 넣을 수 있음

```cs
IEnumerable<int> output = from item in input
                            where item%2==0
                            select item;
```

다만 이는 쿼리와 select 구문에 입력하는 자료형에 따라 굉장히 다양하게 바뀔 수 있으므로

그냥 var 키워드를 사용하는게 가장 안정적이고 편함

하지만 메서드에서 반환하는 경우에는 var 키워드를 지정할 수 없으므로 이런 경우 배열 또는 리스트로 확실히 자료형을 지정하고 싶다면 ToArray() 메서드 또는 ToList() 메서드를 사용해야 함

ToArray() 메서드

```cs
public int[] SelectEven(int[] input)
{
    return (from item in input
            where item%2==0
            select item).ToArray<int>();
}
```

ToList() 메서드

```cs
public List<int> SelectEven(List<int> input)
{
    return (from item in input
            where item%2==0
            select item).ToList<int>();
}
```

<br>

## 익명 객체

C#은 다음과 같은 형식으로 클래스를 만들지 않아도 객체를 생성할 수 있음

이처럼 클래스 이름 없이 생성하는 객체를 익명 객체라고 부름

```cs
new { <속성A> = <값>, <속성B> = <값> };
```

일반적으로는 사용하지 않지만 Linq와 함께 사용할 때 굉장히 큰 효과를 발휘함

<br>

## 익명 객체를 다루는 간단한 예제

Linq의 select 구문에 익명 객체를 활용한 예제

클래스를 따로 선언하지 않고도 객체의 배열을 만들고 활용할 수 있음

```cs
static void Main(string[] args)
{
    List<int> input = new List<int>() { 1, 2, 3, 4, 5, 6, 7, 8, 9, 10 };

    var output = from item in input
                    where item%2==0
                    select new
                    {
                        A = item*2,
                        B = item*item,
                        C = 100
                    };
    
    foreach (var item in output)
    {
        Console.WriteLine(item.A);
        Console.WriteLine(item.B);
        Console.WriteLine(item.C);
        Console.WriteLine();
    }
}
```

```
4
4
100

8
16
100

12
36
100

16
64
100

20
100
100
```

<br>

## Linq 구문과 클래스 활용

클래스를 활용한 Linq

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
        List<Product> input = new List<Product>()
        {
            new Product() { Name = "고구마", Price = 1500 },
            new Product() { Name = "사과", Price = 2400 },
            new Product() { Name = "바나나", Price = 1000 },
            new Product() { Name = "배", Price = 3000 },
            new Product() { Name = "감자", Price = 1000 },
            new Product() { Name = "토마토", Price = 2000 },
            new Product() { Name = "옥수수", Price = 1500 },
            new Product() { Name = "자두", Price = 500 }
        };

        var output = from item in input
                        where item.Price>1500
                        orderby item.Name ascending
                        select item;

        foreach (var item in output)
        {
            Console.WriteLine(item);
        }
    }
}
```

```
배 : 3000원
사과 : 2400원
토마토 : 2000원
```

<br>

## Linq to XML

웹에서 XML 가져오기

```cs
using System.Xml.Linq;

class Program
{
    static void Main(string[] args)
    {
        string url = "http://www.kma.go.kr/wid/queryDFSRSS.jsp?zone=1150061500";
        XElement xElement = XElement.Load(url);
        Console.WriteLine(xElement);
    }
}
```

XML 파싱 기본

파싱 (Parsing) = 구문 분석 (데이터를 원하는 형태로 변환하는 것)

```cs
static void Main(string[] args)
{
    string url = "http://www.kma.go.kr/wid/queryDFSRSS.jsp?zone=1150061500";
    XElement xElement = XElement.Load(url);
    var xmlQuery = from item in xElement.Descendants("data")
                    select item;
    
    foreach (var item in xmlQuery)
    {
        Console.WriteLine(item);
    }
}
```

내부 태그 추출

```cs
static void Main(string[] args)
{
    string url = "http://www.kma.go.kr/wid/queryDFSRSS.jsp?zone=1150061500";
    XElement xElement = XElement.Load(url);
    var xmlQuery = from item in xElement.Descendants("data")
                    select item;
    
    foreach (var item in xmlQuery)
    {
        Console.Write(item.Element("hour").Value + "\t");
        Console.Write(item.Element("day").Value + "\t");
        Console.Write(item.Element("temp").Value + "\t");
        Console.Write(item.Element("wdKor").Value + "\t");
        Console.Write(item.Element("wfKor").Value + "\t");
        Console.Write(item.Element("tmn").Value + "\t");
        Console.Write(item.Element("tmx").Value + "\t");
        Console.WriteLine();
    }
}
```

익명 객체 사용

```cs
static void Main(string[] args)
{
    string url = "http://www.kma.go.kr/wid/queryDFSRSS.jsp?zone=1150061500";
    XElement xElement = XElement.Load(url);
    var xmlQuery = from item in xElement.Descendants("data")
                    select new
                    {
                        Hour = item.Element("hour").Value,
                        Day = item.Element("day").Value,
                        Temp = item.Element("temp").Value,
                        WdKor = item.Element("wdKor").Value,
                        WfKor = item.Element("wfKor").Value,
                        Tmn = item.Element("tmn").Value,
                        Tmx = item.Element("tmx").Value
                    };
    
    foreach (var item in xmlQuery)
    {
        Console.Write(item.Hour + "\t");
        Console.Write(item.Day + "\t");
        Console.Write(item.Temp + "\t");
        Console.Write(item.WdKor + "\t");
        Console.Write(item.WfKor + "\t");
        Console.Write(item.Tmn + "\t");
        Console.Write(item.Tmx + "\t");
        Console.WriteLine();
    }
}
```

클래스 활용

```cs
class Program
{
    class Weather
    {
        public string Hour { get; set; }
        public string Day { get; set; }
        public string Wf { get; set; }
        public string Temp { get; set; }
        public string WdKor { get; set; }
        public string WfKor { get; set; }
        public string Tmn { get; set; }
        public string Tmx { get; set; }
    }

    static void Main(string[] args)
    {
        string url = "http://www.kma.go.kr/wid/queryDFSRSS.jsp?zone=1150061500";
        XElement xElement = XElement.Load(url);
        var xmlQuery = from item in xElement.Descendants("data")
                        select new Weather()
                        {
                            Hour = item.Element("hour").Value,
                            Day = item.Element("day").Value,
                            Temp = item.Element("temp").Value,
                            WdKor = item.Element("wdKor").Value,
                            WfKor = item.Element("wfKor").Value,
                            Tmn = item.Element("tmn").Value,
                            Tmx = item.Element("tmx").Value
                        };

        foreach (var item in xmlQuery)
        {
            Console.Write(item.Hour + "\t");
            Console.Write(item.Day + "\t");
            Console.Write(item.Temp + "\t");
            Console.Write(item.WdKor + "\t");
            Console.Write(item.WfKor + "\t");
            Console.Write(item.Tmn + "\t");
            Console.Write(item.Tmx + "\t");
            Console.WriteLine();
        }
    }
}
```

XML 속성 추출

```cs
item.Attribute("속성 이름").Value
item.Attribute["속성 이름"].Value
```
