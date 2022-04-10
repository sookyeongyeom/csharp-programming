# C# 프로그래밍 - CH7 상속과 다형성

## 상속과 다형성

반복을 줄이기 위해 만들어진 방법

<br>

## 상속과 다형성을 사용하지 않은 예

Dog 클래스

```cs
class Dog
{
    public int Age { get; set; }
    public string Color { get; set; }

    public Dog() { this.Age = 0; }

    public void Eat() { Console.WriteLine("냠냠 먹습니다"); }
    public void Sleep() { Console.WriteLine("쿨쿨 잠을 잡니다"); }
    public void Bark() { Console.WriteLine("왈왈 짖습니다"); }
}
```

Cat 클래스

```cs
class Cat
{
    public int Age { get; set; }

    public Cat() { this.Age = 0; }

    public void Eat() { Console.WriteLine("냠냠 먹습니다"); }
    public void Sleep() { Console.WriteLine("쿨쿨 잠을 잡니다"); }
    public void Meow() { Console.WriteLine("냥냥 웁니다"); }
}
```

Dog 클래스와 Cat 클래스의 인스턴스를 만들고 메서드 실행

```cs
static void Main(string[] args)
{
    List<Dog> Dogs = new List<Dog>() { new Dog(), new Dog(), new Dog() };
    List<Cat> Cats = new List<Cat>() { new Cat(), new Cat(), new Cat() };

    foreach (var item in Dogs)
    {
        item.Eat();
        item.Sleep();
        item.Bark();
    }

    foreach (var item in Cats)
    {
        item.Eat();
        item.Sleep();
        item.Meow();
    }
}
```

문제 → 의미 없이 반복되는 부분이 굉장히 많음 (유지보수에도 적합하지 않음)

해결책 → 상속과 다형성

<br>

## 상속

`자식 클래스``:``부모 클래스`

클래스 사이에 부모 자식 관계를 정의하는 작업

Animal 클래스 (부모 클래스)

```cs
class Animal
{
    public int Age { get; set; }

    public void Animal() { this.Age = 0; }

    public void Eat() { Console.WriteLine("냠냠 먹습니다."); }
    public void Sleep() { Console.WriteLine("쿨쿨 잠을 잡니다"); }
}
```

Dog 클래스와 Cat 클래스 (자식 클래스)

```cs
class Dog : Animal
{
    public string Color { get; set; }

    public void Bark() { Console.WriteLine("왈왈 짖습니다."); }
}

class Cat : Animal
{
    public void Meow() { Console.WriteLine("냥냥 웁니다."); }
}
```

자식 클래스는 부모 클래스의 public 또는 protected 멤버에 접근할 수 있음

<br>

## 다른 접근 제한자

|접근 제한자|내부 클래스|외부 클래스|파생 클래스|프로젝트|
|:------:|:------:|:------:|:------:|:------:|
|public|O|O|O|O|
|internal|O|O|O||
|protected|O||O||
|private|O||||
|protected internal|O|같은 어셈블리 안에 있을 때 접근 가능|O||

<br>

## base 키워드

부모 자식 간 멤버 이름이 겹치는 등의 특수한 이유(하이딩 등)로 인해 부모의 메서드에 접근할 수 없을 때,

`this` 키워드와 같은 형태로 `base` 키워드를 사용함

`this`가 자신을 나타내는 키워드라면 `base`는 부모를 나타내는 키워드임

<br>

## protected 접근 제한자

`private` 과 비슷하지만 상속한 클래스(파생 클래스)에서는 접근할 수 있음

<br>

## 다형성

하나의 클래스가 여러 형태로 변환될 수 있는 성질 (=자식 클래스가 부모 클래스로 위장하는 것)

```cs
Animal dog = new Dog();
Animal cat = new Cat();
```

실제 들어있는 것은 각각 Dog과 Cat이지만, 외관상으로는 Animal 클래스이므로 사용할 수 있는 멤버는 Animal 클래스의 멤버 뿐임

<br>

## 부모 클래스로 위장함으로써 얻을 수 있는 효익

하나의 Animal 배열 또는 리스트에 여러 Dog 클래스와 Cat 클래스를 넣을 수 있음

```cs
List<Animal> Animals = new List<Animal>()
{
    new Dog(), new Cat(), new Cat(), new Dog(),
    new Dog(), new Cat(), new Dog(), new Dog()
};

foreach (var item in Animals)
{
    item.Eat();
    item.Sleep();
}
```

<br>

## 부모 클래스로 위장한 자식이 자식 클래스에 있는 메서드를 사용하려면?

자식 클래스로 자료형 변환을 해주어야 함

<br>

## 최상위 클래스

C#에서 만드는 모든 클래스는 Object 라는 클래스의 상속을 받게 됨

즉, 다형성을 활용하여 다음과 같이 사용할 수 있음

```cs
List<Object> listOfObject = new List<Object>();
listOfObject.Add(new Dog());
listOfObject.Add(new Cat());
```

마찬가지로 int, float 자료형 등도 모두 Object 클래스의 상속을 받으므로 다음과 같이 사용할 수도 있음

```cs
List<Object> listOfObject = new List<Object>();
listOfObject.Add(new Dog());
listOfObject.Add(new Cat());
listOfObject.Add(52);
listOfObject.Add(52.273f);
```

<br>

## is 키워드

`객체` `is` `클래스`

특정한 객체가 어떤 클래스인지 확인하기 위한 키워드

```cs
static void Main(string[] args)
{
    List<Animal> Animals = new List<Animal>() { };

    foreach (var item in Animals)
    {
        item.Eat();
        item.Sleep();

        if (item is Dog) { }
        if (item is Cat) { }
    }
}
```

변수 item 이 Dog 클래스라면 다음의 경우 모두 `true` 를 출력하게 됨

```cs
item is Dog
item is Animal
item is Object
```

<br>

## 일반적인 자료형 변환

`(클래스)` `변수`

변환에 실패하면 예외가 발생함

```cs
foreach (var item in Animals)
{
    item.Eat();
    item.Sleep();

    if (item is Dog) { ((Dog)item).Bark(); }
    if (item is Cat) { ((Cat)item).Meow(); }
}
```

<br>

## as 키워드로 자료형 변환

`변수` `as` `클래스`

변환에 실패하면 `null` 을 넣어줌

```cs
foreach (var item in Animals)
{
    item.Eat();
    item.Sleep();

    var dog = item as Dog;
    if (dog!=null) { dog.Bark(); }

    var cat = item as Cat;
    if (cat!=null) { cat.Meow(); }
}
```

<br>

## 상속의 생성자

자식 인스턴스를 생성하면, 부모가 가지고 있는 멤버의 초기화를 위해 부모 생성자도 자동으로 호출됨

이 때, 호출되는 순서는 `부모 생성자` → `자식 생성자` 임

부모 생성자 호출을 명시적으로 지정하고 싶을 때는 `base()` 키워드를 사용함

다음과 같이 부모 생성자가 오버로딩되어있는 경우가 한 가지 예라고 할 수 있음

```cs
class Program
{
    class Parent
    {
        public Parent() { Console.WriteLine("Parent()"); }
        public Parent(int param) { Console.WriteLine("Parent(int param)"); }
        public Parent(string param) { Console.WriteLine("Parent(string param)"); }
    }

    class Child : Parent
    {
        public Child() : base(10)
        {
            Console.WriteLine("Child() : base(10)");
        }

        public Child(string input) : base(input)
        {
            Console.WriteLine("Child(string input) : base(input)");
        }
    }

    static void Main(string[] args)
    {
        Child childA = new Child();
        Child childB = new Child("string");
    }
}
```

<br>

## 클래스 변수 상속

클래스 변수는 상속되어도 부모 자식 클래스 간 공유되는 개념이기 때문에 각 클래스에서 같은 변수에 대해 같은 조작을 가하게 되면 변동값은 두 배가 된다.

<br>

## 섀도잉과 하이딩

변수에 같은 이름을 사용하면 이름 충돌이 발생하게 됨

이름 재사용의 종류는 다음과 같음

1. 오버로딩

2. 오버라이딩

3. 섀도잉

4. 하이딩

5. 업스큐어링

이름을 재사용하면 코드를 이해하기 힘들어지므로 지양하는 것이 좋음

<br>

## 섀도잉

변수의 이름이 겹치면 자신과 가장 가까운 변수를 사용하게 됨

즉, 다음과 같은 경우 출력되는 number 는 메서드 내부의 변수 number 임

```cs
class Program
{
    public static int number = 10;

    static void Main(string[] args)
    {
        int number = 20;
        Console.WriteLine(number);
    }
}
```

이렇듯 특정한 영역에서 이름이 겹쳐 다른 변수를 가리는 것을 `섀도잉` 이라고 부름

어떤 대상이 섀도잉되면 일반적인 방법으로는 가려진 변수에 접근할 수 없음

<br>

## 하이딩

부모 클래스와 자식 클래스 간 동일한 이름의 멤버가 생성되었을 시 섀도잉과 같은 현상이 일어나는 것을 `하이딩`이라고 부름

즉, 다음과 같은 경우 출력되는 variable 은 자식 클래스의 변수 variable 임

```cs
class Program
{
    class Parent
    {
        public int variable = 273;
    }

    class Child : Parent
    {
        public string variable = "hiding";
    }

    static void Main(string[] args)
    {
        Child child = new Child();
        Console.WriteLine(Child.variable);
    }
}
```

하이딩을 하게 되면 정상적인 상속을 막아버릴 수 있음

이 경우 만약 부모 클래스에 있는 int 자료형의 변수를 사용하고 싶다면,

다음과 같이 부모로 자료형을 변환한 후 사용하면 됨

```cs
static void Main(string[] args)
{
    Child child = new Child();
    Console.WriteLine(((Parent)child).variable);
}
```

<br>

## 메서드 하이딩

메서드는 변수와 다르게 충돌이 발생할 때 하이딩할지 오버라이딩할지를 결정할 수 있음

<br>

## 하이딩과 오버라이딩

부모 클래스와 자식 클래스 멤버의 이름을 동일하게 작성할 때 하이딩 또는 오버라이딩이 일어나므로 두 경우를 명확하게 구분해주어야 함

하이딩은 멤버 전체(변수, 메서드 등)에서 모두 일어나지만, 오버라이딩은 메서드와 관련되어서만 일어남

<br>

## new 메서드를 사용한 하이딩

하이딩 = 같은 이름으로 멤버를 만들어 부모의 멤버를 숨기는 것

숨겨져 있을 뿐이므로 클래스형을 변환하는 등의 작업을 하면 숨겨진 멤버를 찾을 수 있음

```cs
class Program
{
    class Parent
    {
        public int variable = 273;
        public void Method()
        {
            Console.WriteLine("부모의 메서드");
        }
    }

    class Child
    {
        public new string variable = "hiding";
        public new void Method()
        {
            Console.WriteLine("자식의 메서드");
        }
    }

    static void Main(string[] args)
    {
        Child child = new Child();
        child.Method();
        ((Parent).child).Method();
    }
}
```

new 키워드를 적지 않으면 경고가 발생하지만 실행은 됨

<br>

## virtual 메서드와 override 메서드를 사용한 오버라이딩

오버라이딩 = 부모의 메서드를 덮어씌우는 것

자식의 메서드가 부모의 메서드를 완전히 덮어씌워버리므로, 부모로 클래스형을 변환한다해도 자식에서 다시 정의한 메서드가 호출됨

```cs
class Program
{
    class Parent
    {
        public virtual void Method()
        {
            Console.WriteLine("부모의 메서드");
        }
    }

    class Child : Parent
    {
        public override void Method()
        {
            Console.WriteLine("자식의 메서드");
        }
    }

    static void Main(string[] args)
    {
        Child child = new Child();
        child.Method();
        ((Parent)child).Method();
    }
}
```

<br>

## 하이딩과 오버라이딩의 활용

```cs
class Animal
{
    public virtual void Eat()
    {
        Console.WriteLine("냠냠 먹습니다.");
    }
}

class Dog : Animal
{
    public new void Eat()   // 하이딩
    {
        Console.WriteLine("강아지 사료를 먹습니다.");
    }
}

class Cat : Animal
{
    public override void Eat()  // 오버라이딩
    {
        Console.WriteLine("고양이 사료를 먹습니다.");
    }
}

static void Main(string[] args)
{
    List<Animal> Animals = new List<Animal>()
    {
        new Dog(), new Cat(), new Cat(), new Dog(),
        new Dog(), new Cat(), new Dog(), new Dog()
    };

    foreach (var item in Animals)
    {
        item.Eat();
    }
}
```

```
냠냠 먹습니다.
고양이 사료를 먹습니다.
고양이 사료를 먹습니다.
냠냠 먹습니다.
냠냠 먹습니다.
고양이 사료를 먹습니다.
냠냠 먹습니다.
냠냠 먹습니다.
```

<br>

## 상속과 오버라이딩 제한

클래스에 절대 상속하지 말라거나 반드시 상속하라는 정보를 입력하는 것

또한, 메서드에 더 이상 오버라이딩하지 말라거나 무조건 오버라이딩해달라는 정보를 입력하는 것

<br>

## sealed 키워드

클래스 → 절대 상속하지 말 것

```cs
class Program
{
    sealed class Parent
    {
        public void Test() { }
    }

    class Child : Parent    // 오류 발생
    {
        public void Test() { }
    }
}
```

메서드 → 더 이상 오버라이딩하지 말 것

```cs
class Parent
{
    public virtual void Test() { }
}

class Child : Parent
{
    sealed public override void Test() { }
}

class GrandChild : Child
{
    public override void Test() { }     // 오류 발생
}
```

<br>

## abstract 키워드

클래스 → 반드시 상속해서 쓸 것

해당 클래스 자체는 인스턴스를 만들어 사용할 수 없게 됨

```cs
class Program
{
    abstract class Parent
    {
        public void Test() { }
    }

    class Child : Parent
    {
        public void Test() { }
    }

    static void Main(string[] args)
    {
        Parent parent = new Parent();   // 오류 발생
        Child child = new Child();
    }
}
```

메서드 → 반드시 오버라이딩할 것

`abstract` 키워드를 메서드에 적용하려면 반드시 클래스에도 `abstract` 키워드를 적용해야 함

`abstract` 키워드를 적용한 메서드에는 `{ }` 를 적지 않고 곧바로 세미콜론을 찍음 → 어차피 상속해서 사용할 것이므로 내용을 적지 않는 것

```cs
abstract class Parent
{
    public abstract void Test();
}

class Child : Parent
{
    public override void Test() { }     // 이처럼 오버라이딩해주면 오류가 발생하지 않음
}
```

`abstract` 키워드를 적용했다면 `virtual` 키워드는 적어주지 않아도 됨 (입력 시 오류 발생)
