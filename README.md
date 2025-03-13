## Дневник по C# (платформа .NET).

<details><summary>Содержание</summary>
  
- <details><summary>Документация по C#</summary>
  <ul>
      <li><a href="#введение-в-c">Введение в C#</a></li>
      <li><a href="#основы-программирования">Основы программирования</a></li>
      <li><a href="#ооп-и-все-что-с-ним-связано">ООП и все что с ним связано</a></li>
      <li><a href="#обобщения">Обобщения</a></li>
      <li><a href="#делегаты">Делегаты</a></li>
      <li><a href="#интерфейсы">Интерфейсы</a></li>
      <li><a href="#паттерны">Паттерны</a></li>
      <li><a href="#коллекции">Коллекции</a></li>
      <li><a href="#ссылки-на-литературу">Ссылки на литературу</a></li>
  </ul>
  </details>

</details>

### Введение

### Основы

### ООП и все что с ним связано
<details><summary>Классы и объекты</summary>
Описанием объекта является класс, а объект представляет экземпляр этого класса. Можно еще провести следующую аналогию. У нас у всех есть некоторое представление о человеке, у которого есть имя, возраст, какие-то другие характеристики. То есть некоторый шаблон - этот шаблон можно назвать классом. Конкретное воплощение этого шаблона может отличаться, например, одни люди имеют одно имя, другие - другое имя. И реально существующий человек (фактически экземпляр данного класса) будет представлять объект этого класса.

```csharp
class название_класса
{
    // содержимое класса
}
```
- Поля и методы в классе
```csharp
class Person 
{
    public string name = "Undefined";   // Поле для имени
    public int age;                     // Поле для возвраста
 
    public void Print() // Метод
    {
        Console.WriteLine($"Имя: {name}  Возраст: {age}");
    }
}
```
- Конструкторы
В классе можно реализовать конструкторы котогрые при создании экземпляра класса будут производить какие-нибудь действия.
```csharp
class Person {
    public string name;
    public int age;
    public Person() {
        Console.WriteLine("Создание объекта Person");
        name = "Tom";
        age = 37;
    }
}
```

Так же существуют конструкторы по умолчанию, это такие конструкторы который не принимает никаких параметров.
```csharp
Person tom = new Person();  // создание объекта класса Person
 
// определение класса Person
class Person 
{
    public string name = "Undefined";
    public int age;
 
    public void Print()
    {
        Console.WriteLine($"Имя: {name}  Возраст: {age}");
    }
}
```

- Создание объекта(экземпляра) класса
```csharp
new конструктор_класса(параметры_конструктора);
```

- Обращение к функционалу
```csharp
экземпляр_класса.поле_класса
экземпляр_класса.метод_класса(параметры_метода)
```
```csharp
Person tom = new Person();  // создание объекта класса Person
 
// Получаем значение полей в переменные
string personName = tom.name;
int personAge = tom.age;
Console.WriteLine($"Имя: {personName}  Возраст {personAge}");   // Имя: Undefined  Возраст: 0
 
// устанавливаем новые значения полей
tom.name = "Tom";
tom.age = 37;
 
// обращаемся к методу Print
tom.Print();    // Имя: Tom  Возраст: 37
 
class Person 
{
    public string name = "Undefined";
    public int age;
 
    public void Print()
    {
        Console.WriteLine($"Имя: {name}  Возраст: {age}");
    }
}
```
</details>

<details><summary>Структуры</summary>
Такие типы как например int, double и т.д., по сути являются структурами. Для определения структуры применяется ключевое слово struct  
  
```csharp
struct имя_структуры
{
    // элементы структуры
}
```
  
В структуре как и в классах есть возможность хранить поля, определять методы и т.д.
```csharp
struct Person
{
    public string name;
    public int age;
    public void Print()
    {
        Console.WriteLine($"Имя: {name}  Возраст: {age}");
    }
}
```
Самый важный вопрос **в чем отличие структуры от класса**:
- Структуры являются типом значений и хранятся в стеке, в то время как классы являются ссылочным типом и ссылка на кучу в котогрой хранится класс находится в стеке.
- Структуры не могут наследоваться,т.к. не являются ссылочным типом, в отличии от классов у которых есть возможность наследования.
</details>


<details><summary>Что такое ООП и его основные принципы</summary>

**ООП** — это модель программирования, основными концепциями которой являются понятия объекта и класса. ООП даёт возможность создавать программы, ориентированные на объекты и их взаимодействие между собой, что делает код более организованным, гибким и лёгким в поддержке и модификации.

#### Основные принципы ООП:
1. **Инкапсуляция**  
   Это процесс сокрытия внутренней реализации объекта и предоставления доступа к его данным только через определённые методы или свойства.

Пример:
```csharp
public class Person
{
    private string name;
    public string Name
    {
        get { return name; }
        set { if (!string.IsNullOrEmpty(value)) name = value; }
    }
    private int age;
    public int Age
    {
        get { return age; }
        private set { if (value > 0) age = value; }
    }
    public Person(string name, int age)
    {
        Name = name;
        Age = age;
    }
    public void CelebrateBirthday()
    {
        Age++;
    }
}
```

2. **Наследование**  
   Это механизм, позволяющий создавать новые классы на основе уже существующих. Т.е. новый класс (наследник) может наследовать свойства и методы родительского класса, а также добавлять.

Пример:
```csharp
class Person
{
    public string Name { get; set;}
    public Person(string name)
    {
        Name = name;
    }
    public void Print()
    {
        Console.WriteLine(Name);
    }
}
 
class Employee : Person
{
    public string Company { get; set; }
    public Employee(string name, string company)
        : base(name)
    {
        Company = company;
    }
}
```
Но есть свои ограничения, а именно:  
- Классы множественное наследование, класс может наследоваться только от одного класса.
- При создании производного класса надо учитывать тип доступа к базовому классу - тип доступа к производному классу должен быть таким же, как и у базового класса, или более строгим. То есть, если базовый класс у нас имеет тип доступа internal, то производный класс может иметь тип доступа internal или private, но не public. Однако следует также учитывать, что если базовый и производный класс находятся в разных сборках (проектах), то в этом случае производый класс может наследовать только от класса, который имеет модификатор public.
- Если класс объявлен с модификатором sealed, то от этого класса нельзя наследовать и создавать производные классы.  

3. **Полиморфизм**  
   Это возможность одного метода или оператора иметь несколько форм или реализаций, в зависимости от типа объекта. Таким образом, разные объекты могут использовать одинаковые методы или свойства, но при этом они будут использоваться по-разному.

Пример:
```csharp
// Базовый класс
public class Animal
{
    // Виртуальный метод, который может быть переопределён
    public virtual void Speak()
    {
        Console.WriteLine("Animal makes a sound.");
    }

    // Невиртуальный метод - нельзя переопределить
    public void Eat()
    {
        Console.WriteLine("Animal is eating.");
    }
}

// Производный класс Dog
public class Dog : Animal
{
    // Переопределение виртуального метода
    public override void Speak()
    {
        Console.WriteLine("Dog barks.");
    }
}

// Производный класс Cat
public class Cat : Animal
{
    // Переопределение виртуального метода
    public override void Speak()
    {
        Console.WriteLine("Cat meows.");
    }
}

// Интерфейс
public interface IAnimalActions
{
    void Sleep(); // Метод интерфейса
}

// Производный класс Bird, реализующий интерфейс
public class Bird : Animal, IAnimalActions
{
    public override void Speak()
    {
        Console.WriteLine("Bird chirps.");
    }

    // Реализация метода интерфейса
    public void Sleep()
    {
        Console.WriteLine("Bird is sleeping.");
    }
}
```
4. **Астракция**  
   Это способ выделения общей сущности из множества конкретных объектов. Абстракция позволяет сконцентрироваться на существенных характеристиках объекта, а не на его деталях реализации. Через абстракцию создаются интерфейсы, которые могут быть использованы для обращения к различным объектам.
</details>

### Делегаты

<details><summary>Делегаты и их применение</summary>
Делегаты представляют такие объекты, которые указывают на методы. То есть делегаты - это указатели на методы и с помощью делегатов мы можем вызвать данные методы.

- Инициализация делегата
```csharp
Message mes;            // 2. Создаем переменную делегата
mes = Hello;            // 3. Присваиваем этой переменной адрес метода
mes();                  // 4. Вызываем метод
 
void Hello() => Console.WriteLine("Hello METANIT.COM");
 
delegate void Message(); // 1. Объявляем делегат
```
При этом делегаты необязательно могут указывать только на методы, которые определены в том же классе, где определена переменная делегата. Это могут быть также методы из других классов и структур.
```csharp
Message message1 = Welcome.Print;
Message message2 = new Hello().Display;
 
message1(); // Welcome
message2(); // Привет
 
delegate void Message();
 
class Welcome
{
    public static void Print() => Console.WriteLine("Welcome");
}
class Hello
{
    public void Display() => Console.WriteLine("Привет");
}
```
Рассмотрим определение и применение делегата, который принимает параметры и возвращает результат.
```csharp
Operation operation = Add;      // делегат указывает на метод Add
int result = operation(4, 5);   // фактически Add(4, 5)
Console.WriteLine(result);      // 9
     
operation = Multiply;           // теперь делегат указывает на метод Multiply
result = operation(4, 5);       // фактически Multiply(4, 5)
Console.WriteLine(result);      // 20
 
int Add(int x, int y) => x + y;
 
int Multiply(int x, int y) => x * y;
 
delegate int Operation(int x, int y);
```
Важное замечение, мы не можем присоить (добавить) ссылку на метод если у метода сиогнатура отличная от сигнатуры делегата.
```csharp
delegate void SomeDel(int a, double b); // существует такой делегат
void SomeMethod1(int g, double n) { } // пускай у нас есть такой метод
SomeDel gooddel = SomeMethod1; // в данном случае сигнатура метода и делегата одинаковые
// остальные же методы не соответсвуют сигнатуре 
double SomeMethod2(int g, double n) { return g + n; }
void SomeMethod3(double n, int g) { }
void SomeMethod4(ref int g, double n) { }
void SomeMethod5(out int g, double n) { g = 6; }

```
- Добавление ссылки и удаление ссылкина метод
Добавление ссылки на метод происходит при помощи операции "+=".
```csharp
Message message = Hello;
message += HowAreYou;  // теперь message указывает на два метода
message();              // вызываются оба метода - Hello и HowAreYou
 
void Hello() => Console.WriteLine("Hello");
void HowAreYou() => Console.WriteLine("How are you?");
 
delegate void Message();
```
Удаление ссылки на метод происходит при помощи операции "-=".
При удалении следует учитывать, что если делегат содержит несколько ссылок на один и тот же метод, то операция -= начинает поиск с конца списка вызова делегата и удаляет только первое найденное вхождение.
```csharp
Message? message = Hello; 
message += HowAreYou;
message();  // вызываются все методы из message
message -= HowAreYou;   // удаляем метод HowAreYou
if (message != null) message(); // вызывается метод Hello
```
Важно учесть что список вызовов делегата может быть пустым, в таком случает ему присваивается значение null. Поэтому при вызове делегата лучше сего использовать .Invoke, т.к. он не вызовит исключение, как, например, в следующем случае.

Вызов делегата без использования Invoke
```csharp
Message? mes;
//mes();        // ! Ошибка: делегат равен null
 
Operation? op = Add;
op -= Add;      // делегат op пуст
int n = op(3, 4);       // !Ошибка: делегат равен null
```

Вызов делегата с использованием Invoke
```csharp
Message? mes = null;
mes?.Invoke();        // ошибки нет, делегат просто не вызывается
 
Operation? op = Add;
op -= Add;          // делегат op пуст
int? n = op?.Invoke(3, 4);   // ошибки нет, делегат просто не вызывается, а n = null
```
- Обобщенные делегаты
```csharp
Operation<decimal, int> squareOperation = Square; // в данном случае у нас на выход подается переменная типа decimal, а на вход int
decimal result1 = squareOperation(5); // вызов делегата
Console.WriteLine(result1);  // 25
 
Operation<int, int> doubleOperation = Double; // в данном случае у нас на выход подается переменная типа int, а на вход int
int result2 = doubleOperation(5);
Console.WriteLine(result2);  // 10
 
decimal Square(int n) => n * n;
int Double(int n) => n + n;
 
delegate T Operation<T, K>(K val); // инициализация обощенного делегата который полуает переменную какого-то типа K и возвращает переменную  какого-то типа T 
```
- Использование делегатов в качестве параметров в методах (функциях)
```csharp
DoOperation(5, 4, Add);         // 9
DoOperation(5, 4, Subtract);    // 1
DoOperation(5, 4, Multiply);    // 20
 
void DoOperation(int a, int b, Operation op)
{
    Console.WriteLine(op(a,b));
}
int Add(int x, int y) => x + y;
int Subtract(int x, int y) => x - y;
int Multiply(int x, int y) => x * y;
 
delegate int Operation(int x, int y);
```
Бывают и такие случаи когда нам небходимо возвращать в качестве результата ссылку на метод как в примере ниже.
```csharp
Operation operation = SelectOperation(OperationType.Add);
Console.WriteLine(operation(10, 4));    // 14
 
operation = SelectOperation(OperationType.Subtract);
Console.WriteLine(operation(10, 4));    // 6
 
operation = SelectOperation(OperationType.Multiply);
Console.WriteLine(operation(10, 4));    // 40
 
Operation SelectOperation(OperationType opType)
{
    switch (opType)
    {
        case OperationType.Add: return Add;
        case OperationType.Subtract: return Subtract;
        default: return Multiply;
    }
}
 
int Add(int x, int y) => x + y;
int Subtract(int x, int y) => x - y;
int Multiply(int x, int y) => x * y;
 
enum OperationType
{
    Add, Subtract, Multiply
}
delegate int Operation(int x, int y);
```
</details>

<details><summary>Анонимные и лямбда функции</summary>

1. **Анонимные функции**
  
  С делегатами тесно связаны анонимные методы. Анонимные методы используются для создания экземпляров делегатов.
  
```csharp
MessageHandler handler = delegate (string mes) // анонимная функция
{
    Console.WriteLine(mes); // инструкции
};
handler("hello world!");
 
delegate void MessageHandler(string message); // инициализация делегата
```
Другой пример анонимных методов - передача в качестве аргумента для параметра, который представляет делегат:
```csharp
ShowMessage("hello!", delegate (string mes)
{
    Console.WriteLine(mes);
});
 
static void ShowMessage(string message, MessageHandler handler)
{
    handler(message);
}
 
delegate void MessageHandler(string message);
```
Если анонимный метод использует параметры, то они должны соответствовать параметрам делегата. Если для анонимного метода не требуется параметров, то скобки с параметрами опускаются. При этом даже если делегат принимает несколько параметров, то в анонимном методе можно вовсе опустить параметры. Но лучше так не делать так ка читаемость кода из-за этого падает.
```csharp
MessageHandler handler = delegate
{
    Console.WriteLine("анонимный метод");
};
handler("hello world!");    // анонимный метод
 
delegate void MessageHandler(string message);
```
2. **Лямбда функции**
Экземпляр делегата так же можно инициализировать при помощи лямбда-выражений. Лямбда-выражения представляют собой упрощенную запись анонимных методов, которые  позволяют создать емкие лаконичные методы. 

Синтаксис лямбда выражений выглядит следующим образом
```csharp
(список_параметров) => выражение // '=>' - это и есть лямбда )))
```
- Лямбда-выражения без параметров
В ниже приведенном примере представленна лямбда-функция которая ничего не принимает и просто выводит слово "Hello" в консоль
```csharp
Message hello = () => Console.WriteLine("Hello");
hello();       // Hello
hello();       // Hello
hello();       // Hello
 
delegate void Message();
```
В случае если лямбда-выражению необходимо выполнить несколько операций, то эти операции помещаются в фигурные скобочки.
```csharp
Message hello = () =>
{
    Console.Write("Hello ");
    Console.WriteLine("World");
};
hello();
```
- Лямбда-выражения которые на вход принимают пармаетры
```csharp
Operation sum = (x, y) => Console.WriteLine($"{x} + {y} = {x + y}");
sum(1, 2);       // 1 + 2 = 3
sum(22, 14);    // 22 + 14 = 36
 
delegate void Operation(int x, int y);
```
В случае если мы применяем неявную типизацию (т.е. инициализируем нашу переменную делегата через var), обязательно надо указать тип параметров.

Неправильный вариант записи.
```csharp
var sum = (x, y) => Console.WriteLine($"{x} + {y} = {x + y}");   // ! Ошибка
```
Правильный вариант записи.
```csharp
var sum = (int x, int y) => Console.WriteLine($"{x} + {y} = {x + y}");
sum(1, 2);       // 1 + 2 = 3
sum(22, 14);    // 22 + 14 = 36
```
Так же лямбда-выражение может быть передана в качестве параметра метода
```csharp
int[] integers = { 1, 2, 3, 4, 5, 6, 7, 8, 9 };
 
// найдем сумму чисел больше 5
int result1 = Sum(integers, x => x > 5);
Console.WriteLine(result1); // 30
 
// найдем сумму четных чисел
int result2 = Sum(integers, x => x % 2 == 0);
Console.WriteLine(result2);  //20
 
int Sum(int[] numbers, IsEqual func)
{
    int result = 0;
    foreach (int i in numbers)
    {
        if (func(i))
            result += i;
    }
    return result;
}
 
delegate bool IsEqual(int x);
```
- Лямбда-ввырадения которые возвращают рузультат
```csharp
var sum = (int x, int y) => x + y;
int sumResult = sum(4, 5);                  // 9
Console.WriteLine(sumResult);               // 9
 
Operation multiply = (x, y) => x * y;
int multiplyResult = multiply(4, 5);        // 20
Console.WriteLine(multiplyResult);          // 20
 
delegate int Operation(int x, int y);
```
В случае если несколько выражений то тогда лябда-выражение будет выглядеть так
```csharp
var subtract = (int x, int y) =>
{
    if (x > y) return x - y;
    else return y - x;
};
int result1 = subtract(10, 6);  // 4 
Console.WriteLine(result1);     // 4
 
int result2 = subtract(-10, 6);  // 16
Console.WriteLine(result2);      // 16
```
В случае же если у нас лямбда-выражение возвращается в качестве результата
```csharp
Operation operation = SelectOperation(OperationType.Add);
Console.WriteLine(operation(10, 4));    // 14
 
operation = SelectOperation(OperationType.Subtract);
Console.WriteLine(operation(10, 4));    // 6
 
operation = SelectOperation(OperationType.Multiply);
Console.WriteLine(operation(10, 4));    // 40
 
Operation SelectOperation(OperationType opType)
{
    switch (opType)
    {
        case OperationType.Add: return (x, y) => x + y;
        case OperationType.Subtract: return (x, y) => x - y;
        default: return (x, y) => x * y;
    }
}
enum OperationType
{
    Add, Subtract, Multiply
}
delegate int Operation(int x, int y);
```
- Добавление и удаление действий в лямбда-выражении
Добавление и удаление дейстий происходит аналогично делегатма, т.е. при помощи "+=" и "-="
```csharp
var hello = () => Console.WriteLine("again");
 
var message = () => Console.Write("Ah shit, ");
message += () => Console.WriteLine("here we go "); // добавляем анонимное лямбда-выражение
message += hello;   // добавляем лямбда-выражение из переменной hello
message += Print;   // добавляем метод
 
message(); // вызов лямбды
Console.WriteLine("--------------"); // для разделения вывода
 
message -= Print;   // удаляем метод
message -= hello;   // удаляем лямбда-выражение из переменной hello
 
message?.Invoke();  // на случай, если в message больше нет действий
 
void Print() => Console.WriteLine("Welcome to C#");
```
</details>

### Интерфейсы
<details><summary>Интерфейсы и их реализация</summary>
&nbsp;&nbsp;&nbsp;Интерфейс представляет некое описание типа, набор компонентов, который должен иметь тип данных. И, собственно, мы не можем создавать объекты интерфейса напрямую с помощью конструктора, как например, в классах. В интерфейсе ни у одного из методов не должно быть тела. Это означает, что в интерфейсе вообще не предоставляется никакой реализации. В нем указывается только, что именно следует делать, но не как это делать. Как только интерфейс будет определен, он может быть реализован в любом количестве классов. Кроме того, в одном классе может быть реализовано любое количество интерфейсов. Для реализации интерфейса в классе должны быть предоставлены тела (т.е. конкретные реализации) методов, описанных в этом интерфейсе. Каждому классу предоставляется полная свобода для определения деталей своей собственной реализации интерфейса. Следовательно, один и тот же интерфейс может быть реализован в двух классах по-разному. Тем не менее в каждом из них должен поддерживаться один и тот же набор методов данного интерфейса. А в том коде, где известен такой интерфейс, могут использоваться объекты любого из этих двух классов, поскольку интерфейс для всех этих объектов остается одинаковым. Благодаря поддержке интерфейсов в C# может быть в полной мере реализован главный принцип полиморфизма: один интерфейс — множество методов.

Инициализация интерфейса выглядит следующим образом
```csharp
interface имя{ // Имя интерфеса обязательно должно начинаться с I
    возвращаемый_тип имя_метода_1 (список_параметров);
    возвращаемый_тип имя_метода_2 (список_параметров);
    // ...
    возвращаемый_тип имя_метода_N (список_параметров);
}
```
В объявлении методов интерфейса используются только их возвращаемый_тип и сигнатура. Они, по существу, являются абстрактными методами. Поэтому все методы интерфейса должны быть реализованы в каждом классе, включающем в себя этот интерфейс. В самом же интерфейсе методы неявно считаются открытыми, поэтому доступ к ним не нужно указывать явно.

Интерфейсы не могут содержать члены данных. В них нельзя также определить конструкторы, деструкторы или операторные методы. Но начиная с версии C# 8.0 интерфейсы поддерживают реализацию методов и свойств по умолчанию. 

- Методы по умолчанию

Допустим, у нас есть куча классов, которые реализуют некоторый интерфейс. Если мы добавим в этот интерфейс новый метод, то мы будем обязаны реализовать этот метод во всех классах, применяющих данный интерфейс. Иначе подобные классы просто не будут компилироваться. Теперь вместо реализации метода во всех классах нам достаточно определить его реализацию по умолчанию в интерфейсе. Если класс не реализует метод, будет применяться реализация по умолчанию.
```csharp
IMovable tom = new Person();
Car tesla = new Car();
tom.Move();     // Walking
tesla.Move();   // Driving
interface IMovable
{
    void Move() => Console.WriteLine("Walking");
}
class Person : IMovable { }
class Car : IMovable
{
    public void Move() => Console.WriteLine("Driving");
}
```
- Модификаторы которые можно использовать в интерфейсах
В интерфейсах можно использовать модификаторы public и internal. По умолчанию в интерфейсах определен модификатор public. В версии C# 11 можно определять статические поля, но они обязательно должны иметь модификатор public или internal.
- Пример реализации интерфейса
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;

namespace ConsoleApplication1
{
    // Создаем два интерфейса, описывающих абстрактные методы 
    // арифметических операций и операций Sqrt и Sqr
    public interface IArOperation
    {
        // Определяем набор абстрактных методов
        int Sum();
        int Otr();
        int Prz();
        int Del();
    }

    public interface ISqrSqrt
    {
        int Sqr(int x);
        int Sqrt(int x);
    }

    // Данный класс реализует интерфейс IArOperation
    class A : IArOperation
    {
        int My_x, My_y;

        public int x
        {
            set { My_x = value; }
            get { return My_x; }
        }

        public int y
        {
            set { My_y = value; }
            get { return My_y; }
        }

        public A() { }
        public A(int x, int y)
        {
            this.x = x;
            this.y = y;
        }

        // Реализуем методы интерфейса
        public virtual int Sum()
        {
            return x + y;
        }

        public int Otr()
        {
            return x - y;
        }

        public int Prz()
        {
            return x * y;
        }

        public int Del()
        {
            return x / y;
        }

        // В данном классе так же можно реализовать собственные методы
        public virtual void rewrite()
        {
            Console.WriteLine("Переменная x: {0}\nПеременная y: {1}",x,y);
        }
    }

    // Данный класс унаследован от класса А, но при этом в нем не нужно
    // заново реализовывать интерфейс, но при этом можно переопределить
    // некоторые его методы
    class Aa : A
    {
        public int z;

        public Aa(int z, int x, int y)
            : base(x, y)
        {
            this.z = z;
        }

        // Переопределим метод Sum
        public override int Sum()
        {
            return base.x + base.y + z;
        }

        public override void rewrite()
        {
            base.rewrite();
            Console.WriteLine("Переменная z: " + z);
        }
    }

    // Данный класс унаследован от класса А, и при этом
    // реализует интерфейс ISqrSqrt
    class Ab : A, ISqrSqrt
    {
        public int Sqr(int x)
        {
            return x * x;
        }

        public int Sqrt(int x)
        {
            return (int)Math.Sqrt((double)(x));
        }
    }

    class Program
    {
        static void Main()
        {
            A obj1 = new A(x: 10, y: 12);
            Console.WriteLine("obj1: ");
            obj1.rewrite();
            Console.WriteLine("{0} + {1} = {2}",obj1.x,obj1.y,obj1.Sum());
            Console.WriteLine("{0} * {1} = {2}", obj1.x, obj1.y, obj1.Prz());
            Aa obj2 = new Aa(z: -3, x: 10, y: 14);
            Console.WriteLine("\nobj2: ");
            obj2.rewrite();
            Console.WriteLine("{0} + {1} + {3} = {2}", obj2.x, obj2.y, obj2.Sum(), obj2.z);

            Console.ReadLine();
        }
    }
}
```





</details> 

### Паттерны
<details><summary>Принципы SOLID</summary></details>

> #### Пораждающие паттерны

<details>
  <summary><b>Фабричный метод (Factory Method)</b></summary>

**Фабричный метод** — это паттерн который определяет интерфейс для создания объекта, позволяя подклассам выбирать, какой класс инстанцировать

**Когда применять:** Когда класс не знает заранее, объекты каких типов ему понадобятся, или когда требуется делегировать создание объектов подклассам.

### 🔹 Пример реализации (C#)

```csharp
  using System;
  
  // Абстрактный создатель
  public abstract class Creator {
      // Фабричный метод
      public abstract IProduct FactoryMethod();
      
      // Клиентский метод, использующий продукт
      public void AnOperation() {
          IProduct product = FactoryMethod();
          product.Operation();
      }
  }
  
  // Интерфейс продукта
  public interface IProduct {
      void Operation();
  }
  
  // Конкретный создатель
  public class ConcreteCreator : Creator {
      public override IProduct FactoryMethod() {
          return new ConcreteProduct();
      }
  }
  
  // Конкретный продукт
  public class ConcreteProduct : IProduct {
      public void Operation() {
          Console.WriteLine("ConcreteProduct operation.");
      }
  }
  
  // Класс для демонстрации вызовов
  public class Program {
      public static void Main() {
          Creator creator = new ConcreteCreator();
          creator.AnOperation();
          // Ожидаемый вывод: ConcreteProduct operation.
      }
  }
```

**Объяснение реализации:** Абстрактный класс Creator определяет метод FactoryMethod(), который реализуется в подклассе ConcreteCreator для создания конкретного продукта. Клиентский метод AnOperation() использует продукт, не зная его конкретного типа.

**Плюсы и минусы:**
Плюсы: расширяемость, слабая связь (слабая связь — это принцип, при котором классы менее зависимы друг от друга) между создателем и продуктом.
Минусы: может привести к увеличению количества классов.

</details>

<details>
  <summary><b>Абстрактная фабрика (Abstract Factory)</b></summary>

**Абстрактная фабрика** — паттерн предоставляет интерфейс для создания семейств взаимосвязанных объектов без указания их конкретных классов.

**Когда применять:** При необходимости обеспечить совместимость наборов объектов и сменяемость «семейства» продуктов.

### 🔹 Пример реализации (C#)

```csharp
  using System;

  // Интерфейс фабрики
  public interface IAbstractFactory {
      IProductA CreateProductA();
      IProductB CreateProductB();
  }
  
  // Интерфейсы продуктов
  public interface IProductA {
      void FunctionA();
  }
  public interface IProductB {
      void FunctionB();
  }
  
  // Конкретная фабрика
  public class ConcreteFactory1 : IAbstractFactory {
      public IProductA CreateProductA() {
          return new ProductA1();
      }
      public IProductB CreateProductB() {
          return new ProductB1();
      }
  }
  
  // Конкретные продукты
  public class ProductA1 : IProductA {
      public void FunctionA() {
          Console.WriteLine("ProductA1 function.");
      }
  }
  public class ProductB1 : IProductB {
      public void FunctionB() {
          Console.WriteLine("ProductB1 function.");
      }
  }
  
  // Класс для демонстрации вызовов
  public class Program {
      public static void Main() {
          IAbstractFactory factory = new ConcreteFactory1();
          IProductA productA = factory.CreateProductA();
          IProductB productB = factory.CreateProductB();
          productA.FunctionA(); // Ожидаемый вывод: ProductA1 function.
          productB.FunctionB(); // Ожидаемый вывод: ProductB1 function.
      }
  }

```
**Объяснение реализации:** Интерфейс IAbstractFactory задаёт методы создания различных продуктов. Каждая конкретная фабрика (например, ConcreteFactory1) создаёт набор продуктов, гарантируя их совместимость.

**Плюсы и минусы:**

Плюсы: гарантированная совместимость продуктов, лёгкая смена семейств.

Минусы: усложнение кода при добавлении новых типов продуктов.

</details>


<details>
  <summary><b>Строитель (Builder)</b></summary>
  
**Строитель** — это паттерн который разделяет процесс конструирования сложного объекта и его представление, позволяя создавать разные представления, используя один и тот же процесс.

**Когда применять:** Когда создание объекта требует выполнения ряда шагов, и разные реализации могут создавать объекты с различной структурой.

### 🔹 Пример реализации (C#)

```csharp
  using System;
  using System.Collections.Generic;
  
  // Продукт – сложный объект
  public class Product {
      public List<string> Parts = new List<string>();
      public void Show() {
          Console.WriteLine(string.Join(", ", Parts));
      }
  }
  
  // Абстрактный строитель (задает поля)
  public abstract class Builder {
      protected Product product = new Product();
      public abstract void BuildPartA();
      public abstract void BuildPartB();
      public Product GetProduct() {
          return product;
      }
  }
  
  // Конкретный строитель (реализует интерфейс как ему надо)
  public class ConcreteBuilder : Builder {
      public override void BuildPartA() {
          product.Parts.Add("PartA");
      }
      public override void BuildPartB() {
          product.Parts.Add("PartB");
      }
  }
  
  // Директор, управляющий процессом строительства (реализует логику заданную строителем)
  public class Director {
      public void Construct(Builder builder) {
          builder.BuildPartA();
          builder.BuildPartB();
      }
  }
  
  // Класс для демонстрации вызовов
  public class Program {
      public static void Main() {
          Builder builder = new ConcreteBuilder();
          Director director = new Director();
          director.Construct(builder);
          Product product = builder.GetProduct();
          product.Show(); // Ожидаемый вывод: PartA, PartB
      }
  }

```

**Объяснение реализации:** Строитель инкапсулирует пошаговый процесс создания объекта. Директор управляет процессом, а конкретный строитель определяет детали сборки.

**Плюсы и минусы:**

Плюсы: гибкость создания, изоляция процесса конструирования.

Минусы: добавление дополнительных классов, усложнение структуры.
</details>

<details>
  <summary><b>Прототип (Prototype)</summary>

**Прототип** — это паттерн который создает объекты, копируя существующий экземпляр-прототип вместо создания нового с нуля.

**Когда применять:** Когда создание объекта затратно, и можно склонировать уже существующий экземпляр.

### 🔹 Пример реализации (C#)

```csharp
using System;

// Абстрактный прототип
public abstract class Prototype {
    public abstract Prototype Clone();
}

// Конкретный прототип
public class ConcretePrototype : Prototype {
    public int Field;
    public override Prototype Clone() {
        // Используем поверхностное копирование
        return (Prototype)this.MemberwiseClone();
    }
}

// Класс для демонстрации вызовов
public class Program {
    public static void Main() {
        ConcretePrototype prototype1 = new ConcretePrototype() { Field = 42 };
        ConcretePrototype prototype2 = (ConcretePrototype)prototype1.Clone();
        Console.WriteLine(prototype2.Field); // Ожидаемый вывод: 42
    }
}
```

**Объяснение реализации:** Метод Clone() выполняет копирование объекта (обычно поверхностное). Это позволяет быстро создавать новые объекты с тем же состоянием.

**Плюсы и минусы:** 

Плюсы: упрощённое создание, уменьшение зависимости от классов.

Минусы: сложности с глубоким копированием, проблемы при наличии ссылок на внешние объекты.

</details>

<details>
  <summary><b>Одиночка (Singleton)</b></summary>
  
**Одиночка** — это паттерн который гарантирует, что у класса есть только один экземпляр, и предоставляет к нему глобальную точку доступа.

**Когда применять:** Когда нужен единственный объект (например, для управления общими ресурсами или конфигурацией).

### 🔹 Пример реализации (C#)

```csharp
/// <summary>
/// База данных разделов. Реализация паттерна Singleton.
/// </summary>
public class SectionDatabase
{
        /// <summary>
        /// База данных разделов.
        /// </summary>
        private static SectionDatabase Database = null;

        /// <summary>
        /// Заблокированный объект.
        /// Служит для синхронизации потоков.
        /// </summary>
        private static object LockObject = new object(); 

        /// <summary>
        /// Список разделов.
        /// </summary>
        private List<Section> _sectionsList;

        /// <summary>
        /// Создает хранилище данных разделов.
        /// </summary>
        protected SectionDatabase()
        {
        }
	
        /// <summary>
        /// Инициализация хранилища данных разделов.
        /// </summary>
        /// <returns>Хранилище данных разделов.</returns>
        public static SectionDatabase Initialize()
        {
            if (Database == null)
            {
                lock (LockObject)
                {
                    if (Database == null)
                    {
                        Database = new SectionDatabase();
                    }
                }
            }

            return Database;
        }
}
```

**Объяснение реализации:**  

В данном классе создаем статическое поле, имеющее тот же тип, что и сам класс: SectionDatabase. По умолчанию он будет равен null, так как еще ни разу не был создан экземпляр данного класса.

Создаем заблокированный объект, который мы будем использовать для синхронизации. Это означает, что в критическую область кода потоки будут заходить по очереди.

Создаем список разделов, в который мы будем добавлять созданные разделы.
Создаем защищенный конструктор. Это необходимо для того, чтобы у нас не было возможности вызвать публичный конструктор, так как в этом случае мы не сможем контролировать количество созданных экземпляров класса SectionDatabase.

Добавляем публичный метод Initialize. Его назначение - инициализировать объект базы данных, а также проверять: если объект базы данных уже был создан, то необходимо возврать уже ранее созданный экземпляр. Также не забываем про использование синхронизации для критической секции.


**Плюсы и минусы:** 

Преимущества паттерна Singleton: класс гарантированно имеет только один экземпляр и не более, у нас есть точка доступа к единственному экземпляру (в нашем случае это метод Initialize).

Недостатки: нарушение принципа единой ответственности (Single Responsibility Principle), требуется особая обработка в многопоточной среде.

</details>


> #### Поведенческие паттерны

<details>
  <summary><b>Стратегия (Strategy)</b></summary>

**Стратегия** — это поведенческий шаблон проектирования, который определяет семейство алгоритмов, инкапсулирует каждый из них и делает их взаимозаменяемыми.

**Когда применять:** Когда необходимо выбирать алгоритм поведения во время выполнения.

### 🔹 Пример реализации (C#)

```csharp
// Интерфейс стратегии
public interface IStrategy {
    void Execute();
}

public class ConcreteStrategyA : IStrategy {
    public void Execute() {
        Console.WriteLine("Strategy A executed.");
    }
}

// Контекст, использующий стратегию
public class Context {
    private IStrategy strategy;
    public Context(IStrategy strategy) {
        this.strategy = strategy;
    }
    public void SetStrategy(IStrategy strategy) {
        this.strategy = strategy;
    }
    public void ExecuteStrategy() {
        strategy.Execute();
    }
}

```
**Объяснение реализации:** Контекст делегирует выполнение алгоритма объекту-стратегии. Замена стратегии происходит без изменения контекста.

**Плюсы и минусы:**

Плюсы: гибкость, расширяемость, простота замены алгоритмов.

Минусы: клиент должен знать о различных стратегиях.
</details>

<details>
  <summary><b>Наблюдатель (Observer)</b></summary>

**Наблюдатель** — это поведенческий шаблон проектирования, который определяет зависимость «один ко многим», позволяя объекту оповещать наблюдателей об изменениях своего состояния.

**Когда применять:** Когда изменение одного объекта должно автоматически отражаться в других.

### 🔹 Пример реализации (C#)

```csharp
using System;
using System.Collections.Generic;

// Интерфейс наблюдателя
public interface IObserver {
    void Update(string message);
}

public class ConcreteObserver : IObserver {
    public void Update(string message) {
        Console.WriteLine("Received: " + message);
    }
}

// Субъект, который отслеживает изменения
public class Subject {
    private List<IObserver> observers = new List<IObserver>();
    public void Attach(IObserver observer) {
        observers.Add(observer);
    }
    public void Detach(IObserver observer) {
        observers.Remove(observer);
    }
    public void Notify(string message) {
        foreach (var observer in observers)
            observer.Update(message);
    }
}

// Класс для демонстрации вызовов
public class Program {
    public static void Main() {
        Subject subject = new Subject();
        IObserver observer = new ConcreteObserver();
        subject.Attach(observer);
        subject.Notify("Hello Observers");
        // Ожидаемый вывод: Received: Hello Observers
    }
}
```
**Объяснение реализации:** Субъект хранит список наблюдателей и оповещает их при изменении состояния. Наблюдатели реализуют метод Update() для получения уведомлений.

**Плюсы и минусы:**

Плюсы: слабая связь между субъектом и наблюдателями, динамическое добавление/удаление.

Минусы: возможны утечки памяти, если наблюдатели не отписываются.
</details>

<details>
  <summary><b>Команда (Command)</b></summary>

**Команда** — это поведенческий шаблон проектирования, который инкапсулирует запрос как объект, позволяя параметризовать объекты, ставить запросы в очередь и поддерживать отмену операций.

**Когда применять:** Когда нужно отделить инициатора команды от её исполнителя, а также реализовать логирование, отложенное выполнение или отмену действий.

### 🔹 Пример реализации (C#)

```csharp
using System;

// Интерфейс команды
public interface ICommand {
    void Execute();
}

// Конкретная команда
public class ConcreteCommand : ICommand {
    private Receiver receiver;
    public ConcreteCommand(Receiver receiver) {
        this.receiver = receiver;
    }
    public void Execute() {
        receiver.Action();
    }
}

// Получатель, выполняющий действие
public class Receiver {
    public void Action() {
        Console.WriteLine("Receiver action performed.");
    }
}

// Инициатор команды
public class Invoker {
    private ICommand command;
    public void SetCommand(ICommand command) {
        this.command = command;
    }
    public void Invoke() {
        command.Execute();
    }
}

// Класс для демонстрации вызовов
public class Program {
    public static void Main() {
        Receiver receiver = new Receiver();
        ICommand command = new ConcreteCommand(receiver);
        Invoker invoker = new Invoker();
        invoker.SetCommand(command);
        invoker.Invoke();
        // Ожидаемый вывод: Receiver action performed.
    }
}
```
**Объяснение реализации:** Команда инкапсулирует действие и хранит ссылку на объект-получатель. Инициатор (Invoker) вызывает команду, не зная деталей выполнения.

**Плюсы и минусы:**

Плюсы: слабая связь между объектами, возможность отмены/повтора операций.

Минусы: увеличение количества классов, усложнение кода.
</details>

<details>
  <summary><b>Шаблонный метод (Template Method)</b></summary>

**Шаблонный метод** — это поведенческий шаблон проектирования, который определяет основу алгоритма, позволяя подклассам переопределять отдельные шаги без изменения структуры алгоритма.

**Когда применять:** Если алгоритм имеет фиксированную структуру, но отдельные шаги могут меняться.

### 🔹 Пример реализации (C#)

```csharp
/using System;

// Абстрактный класс с шаблонным методом
public abstract class AbstractClass {
    public void TemplateMethod() {
        PrimitiveOperation1();
        PrimitiveOperation2();
    }
    protected abstract void PrimitiveOperation1();
    protected abstract void PrimitiveOperation2();
}

// Конкретная реализация
public class ConcreteClass : AbstractClass {
    protected override void PrimitiveOperation1() {
        Console.WriteLine("Operation 1");
    }
    protected override void PrimitiveOperation2() {
        Console.WriteLine("Operation 2");
    }
}

// Класс для демонстрации вызовов
public class Program {
    public static void Main() {
        AbstractClass instance = new ConcreteClass();
        instance.TemplateMethod();
        // Ожидаемый вывод:
        // Operation 1
        // Operation 2
    }
}
```
**Объяснение реализации:** Базовый класс задаёт «скелет» алгоритма, а подклассы реализуют конкретные шаги, позволяя переиспользовать общую логику.

**Плюсы и минусы:**

Плюсы: повторное использование кода, единая структура алгоритма.

Минусы: ограниченная гибкость, если требуется динамически менять последовательность шагов.
</details>

<details>
  <summary><b>Итератор (Iterator)</b></summary>

**Итератор** — это поведенческий шаблон проектирования, который предоставляет способ последовательного доступа к элементам агрегированного объекта, не раскрывая его внутреннюю структуру.

**Когда применять:** При необходимости обойти коллекцию, не предоставляя доступ к её внутреннему устройству.

### 🔹 Пример реализации (C#)

```csharp
using System;
using System.Collections;
using System.Collections.Generic;

// Агрегат, реализующий IEnumerable
public class ConcreteAggregate<T> : IEnumerable<T> {
    private List<T> items = new List<T>();
    public void Add(T item) { items.Add(item); }
    // обощенный метод для воззвращения коллекции
    public IEnumerator<T> GetEnumerator() {
        return items.GetEnumerator();
    }
    // не обобщенный, обязателен в реализации 
    IEnumerator IEnumerable.GetEnumerator() {
        return GetEnumerator();
    }
}

// Класс для демонстрации вызовов
public class Program {
    public static void Main() {
        ConcreteAggregate<int> aggregate = new ConcreteAggregate<int>();
        aggregate.Add(1);
        aggregate.Add(2);
        aggregate.Add(3);
        foreach (var item in aggregate) {
            Console.WriteLine(item);
        }
        // Ожидаемый вывод:
        // 1
        // 2
        // 3
    }
}
```
**Объяснение реализации:** Реализуя IEnumerable<T>, коллекция становится совместимой с оператором foreach, что скрывает детали внутреннего представления.

**Плюсы и минусы:**

Плюсы: простота использования и интеграция с языковыми конструкциями.

Минусы: может скрывать неэффективность итерации в кастомных коллекциях.
</details>

<details>
  <summary><b>Состояние (State)</b></summary>

**Состояние** — это поведенческий шаблон проектирования, который позволяет объекту изменять поведение в зависимости от его внутреннего состояния, словно меняется его класс.

**Когда применять:** Когда объект должен менять своё поведение при изменении состояния, а условные операторы приводят к громоздкому коду.

### 🔹 Пример реализации (C#)

```csharp
using System;

// Интерфейс состояния
public interface IState {
    void Handle(ContextState context);
}

public class ConcreteStateA : IState {
    public void Handle(ContextState context) {
        Console.WriteLine("State A handling.");
        context.State = new ConcreteStateB();
    }
}

public class ConcreteStateB : IState {
    public void Handle(ContextState context) {
        Console.WriteLine("State B handling.");
        context.State = new ConcreteStateA();
    }
}

// Контекст, который делегирует поведение состоянию
public class ContextState {
    public IState State { get; set; }
    public ContextState(IState state) {
        State = state;
    }
    public void Request() {
        State.Handle(this);
    }
}

// Класс для демонстрации вызовов
public class Program {
    public static void Main() {
        ContextState context = new ContextState(new ConcreteStateA());
        context.Request(); // Ожидаемый вывод: State A handling.
        context.Request(); // Ожидаемый вывод: State B handling.
    }
}
```
**Объяснение реализации:** Контекст хранит текущее состояние и делегирует обработку вызова ему. Каждое состояние само определяет, к какому следующему состоянию перейти.

**Плюсы и минусы:**

Плюсы: упрощение логики при множестве состояний, разделение ответственности.

Минусы: увеличение числа классов, усложнение структуры при множестве состояний.
</details>

<details>
  <summary><b>Цепочка обязанностей (Chain of Responsibility)</b></summary>

**Цепочка обязанностей** — это поведенческий шаблон проектирования, который позволяет передавать запрос по цепочке объектов-обработчиков, где каждый решает, обработать запрос или передать дальше.

**Когда применять:** Когда несколько объектов могут обработать запрос, и получатель неизвестен заранее.

### 🔹 Пример реализации (C#)

```csharp
using System;

// Абстрактный обработчик
public abstract class Handler {
    protected Handler next;
    public void SetNext(Handler nextHandler) {
        next = nextHandler;
    }
    public abstract void HandleRequest(int request);
}

public class ConcreteHandler1 : Handler {
    public override void HandleRequest(int request) {
        if (request < 10)
            Console.WriteLine("Handler1 handled request " + request);
        else if (next != null)
            next.HandleRequest(request);
    }
}

public class ConcreteHandler2 : Handler {
    public override void HandleRequest(int request) {
        if (request >= 10)
            Console.WriteLine("Handler2 handled request " + request);
        else if (next != null)
            next.HandleRequest(request);
    }
}

// Класс для демонстрации вызовов
public class Program {
    public static void Main() {
        ConcreteHandler1 handler1 = new ConcreteHandler1();
        ConcreteHandler2 handler2 = new ConcreteHandler2();
        handler1.SetNext(handler2);
        handler1.HandleRequest(5);   // Ожидается обработка в Handler1
        handler1.HandleRequest(15);  // Ожидается обработка в Handler2
    }
}
```
**Объяснение реализации:** Каждый обработчик проверяет возможность обработки запроса. Если не может – передаёт его следующему в цепочке.

**Плюсы и минусы:**

Плюсы: уменьшение связанности, гибкость добавления новых обработчиков.

Минусы: не гарантируется обработка запроса, возможны проблемы с производительностью.
</details>

<details>
  <summary><b>Интерпретатор (Interpreter)</b></summary>

**Интерпретатор** — это поведенческий шаблон проектирования, который определяет грамматику для представления языка и интерпретатор, который выполняет выражения, заданные этой грамматикой.

**Когда применять:** Для реализации небольших языков или выражений, где удобна декларативная интерпретация.

### 🔹 Пример реализации (C#)

```csharp
using System;
using System.Collections.Generic;

// Абстрактное выражение
public abstract class Expression {
    public abstract int Interpret(Dictionary<string, int> context);
}

// Числовое выражение
public class Number : Expression {
    private int value;
    public Number(int value) { this.value = value; }
    public override int Interpret(Dictionary<string, int> context) {
        return value;
    }
}

// Операция сложения
public class Add : Expression {
    private Expression left, right;
    public Add(Expression left, Expression right) {
        this.left = left;
        this.right = right;
    }
    public override int Interpret(Dictionary<string, int> context) {
        return left.Interpret(context) + right.Interpret(context);
    }
}

// Класс для демонстрации вызовов
public class Program {
    public static void Main() {
        // Выражение: 5 + 10
        Expression expression = new Add(new Number(5), new Number(10));
        int result = expression.Interpret(new Dictionary<string, int>());
        Console.WriteLine(result); // Ожидаемый вывод: 15
    }
}
```
**Объяснение реализации:** Каждый класс выражения знает, как интерпретировать себя, позволяя строить дерево разбора для вычисления выражения.

**Плюсы и минусы:**

Плюсы: чёткая структура языка, расширяемость операций.

Минусы: трудности масштабирования для сложных языков.
</details>

<details>
  <summary><b>Посредник (Mediator)</b></summary>

**Посредник** — это поведенческий шаблон проектирования, который инкапсулирует способ взаимодействия множества объектов, избавляя их от прямых ссылок друг на друга.

**Когда применять:** Когда множество компонентов общаются между собой, что приводит к сильной связанности, и требуется централизовать коммуникацию.

### 🔹 Пример реализации (C#)

```csharp
using System;

// Абстрактный посредник
public abstract class Mediator {
    public abstract void Notify(object sender, string eventCode);
}

public class ConcreteMediator : Mediator {
    public Component1 Component1 { get; set; }
    public Component2 Component2 { get; set; }
    public override void Notify(object sender, string eventCode) {
        if (eventCode == "A")
            Component2.DoC();
        else if (eventCode == "B")
            Component1.DoD();
    }
}

public class Component1 {
    private Mediator mediator;
    public Component1(Mediator mediator) { this.mediator = mediator; }
    public void DoA() {
        Console.WriteLine("Component1 does A");
        mediator.Notify(this, "A");
    }
    public void DoD() {
        Console.WriteLine("Component1 does D");
    }
}

public class Component2 {
    private Mediator mediator;
    public Component2(Mediator mediator) { this.mediator = mediator; }
    public void DoB() {
        Console.WriteLine("Component2 does B");
        mediator.Notify(this, "B");
    }
    public void DoC() {
        Console.WriteLine("Component2 does C");
    }
}

// Класс для демонстрации вызовов
public class Program {
    public static void Main() {
        ConcreteMediator mediator = new ConcreteMediator();
        mediator.Component1 = new Component1(mediator);
        mediator.Component2 = new Component2(mediator);
        mediator.Component1.DoA(); // Вызывает DoA и затем DoC через посредника
        mediator.Component2.DoB(); // Вызывает DoB и затем DoD через посредника
    }
}
```
**Объяснение реализации:** Посредник получает уведомления от компонентов и направляет команды другим компонентам, устраняя прямые зависимости между ними.

**Плюсы и минусы:**

Плюсы: уменьшение связанности между объектами, централизованный контроль коммуникаций.

Минусы: риск превращения посредника в «бога-объект», усложнение логики.
</details>

<details>
  <summary><b>Хранитель (Memento)</b></summary>

**Хранитель** — это поведенческий шаблон проектирования, который позволяет сохранить и восстановить состояние объекта без нарушения его инкапсуляции.

**Когда применять:** Когда требуется реализовать функциональность отмены/возврата (undo/redo) или временное сохранение состояния.

### 🔹 Пример реализации (C#)

```csharp
using System;

// Хранитель, сохраняющий состояние
public class Memento {
    public string State { get; private set; }
    public Memento(string state) {
        State = state;
    }
}

// Источник, создающий и восстанавливающий состояние
public class Originator {
    public string State { get; set; }
    public Memento SaveState() {
        return new Memento(State);
    }
    public void RestoreState(Memento memento) {
        State = memento.State;
    }
}

// Опекун, управляющий хранением мементо
public class Caretaker {
    private Memento memento;
    public void Save(Originator originator) {
        memento = originator.SaveState();
    }
    public void Restore(Originator originator) {
        originator.RestoreState(memento);
    }
}

// Класс для демонстрации вызовов
public class Program {
    public static void Main() {
        Originator originator = new Originator();
        originator.State = "State1";
        Caretaker caretaker = new Caretaker();
        caretaker.Save(originator);
        originator.State = "State2";
        Console.WriteLine("Current state: " + originator.State); // Ожидаемый вывод: State2
        caretaker.Restore(originator);
        Console.WriteLine("Restored state: " + originator.State); // Ожидаемый вывод: State1
    }
}
```
**Объяснение реализации:** Объект Originator создаёт объект Memento для сохранения своего состояния, а Caretaker управляет этим сохранением, не нарушая инкапсуляцию.

**Плюсы и минусы:**

Плюсы: сохранение инкапсуляции, простая реализация отмены действий.

Минусы: может потреблять много памяти при сохранении больших состояний.
</details>

<details>
  <summary><b>Посетитель (Visitor)</b></summary>

**Посетитель** — это поведенческий шаблон проектирования, который позволяет определить новую операцию для объектов, не изменяя их классы, вынося операцию в отдельный класс.

**Когда применять:** Когда требуется выполнить операцию над группой разнородных объектов, не изменяя их структуры.

### 🔹 Пример реализации (C#)

```csharp
using System;
using System.Collections.Generic;

// Интерфейс посетителя
public interface IVisitor {
    void Visit(ElementA element);
    void Visit(ElementB element);
}

// Базовый элемент
public abstract class Element {
    public abstract void Accept(IVisitor visitor);
}

public class ElementA : Element {
    public override void Accept(IVisitor visitor) {
        visitor.Visit(this);
    }
}

public class ElementB : Element {
    public override void Accept(IVisitor visitor) {
        visitor.Visit(this);
    }
}

// Конкретный посетитель, реализующий операции
public class ConcreteVisitor : IVisitor {
    public void Visit(ElementA element) {
        Console.WriteLine("Visited ElementA");
    }
    public void Visit(ElementB element) {
        Console.WriteLine("Visited ElementB");
    }
}

// Класс для демонстрации вызовов
public class Program {
    public static void Main() {
        List<Element> elements = new List<Element> { new ElementA(), new ElementB() };
        ConcreteVisitor visitor = new ConcreteVisitor();
        foreach (var element in elements) {
            element.Accept(visitor);
        }
        // Ожидаемый вывод:
        // Visited ElementA
        // Visited ElementB
    }
}

```
**Объяснение реализации:** Каждый элемент принимает посетителя, который выполняет операцию, зависящую от типа элемента, что позволяет добавлять новые операции без изменения классов элементов.

**Плюсы и минусы:**

Плюсы: расширяемость операций, соблюдение принципа открытости/закрытости.

Минусы: изменение интерфейса элементов требует обновления всех посетителей.
</details>


> #### Структурные паттерны

<details>
  <summary><b>Декоратор (Decorator)</b></summary>

**Декоратор** — это структурный шаблон проектирования, который динамически добавляет объекту новые обязанности, оборачивая его в класс-декоратор.

**Когда применять:** Когда нужно добавить или изменить поведение отдельного объекта без влияния на другие экземпляры.

### 🔹 Пример реализации (C#)

```csharp
using System;

// Базовый интерфейс компоента
public interface IComponent {
    void Operation();
}

// Конкретный компонент
public class ConcreteComponent : IComponent {
    public void Operation() {
        Console.WriteLine("ConcreteComponent operation.");
    }
}

// Базовый декоратор
public class Decorator : IComponent {
    protected IComponent component;
    public Decorator(IComponent component) {
        this.component = component;
    }
    public virtual void Operation() {
        component.Operation();
    }
}

// Конкретный декоратор, добавляющий поведение
public class ConcreteDecorator : Decorator {
    public ConcreteDecorator(IComponent component) : base(component) { }
    public override void Operation() {
        base.Operation();
        Console.WriteLine("Additional behavior.");
    }
}

// Класс для демонстрации вызовов
public class Program {
    public static void Main() {
        IComponent component = new ConcreteComponent(); // Конкретный объект который модифицируем
        IComponent decorated = new ConcreteDecorator(component); // Декоратор который модифицирует конкретный объект
        decorated.Operation();
        // Ожидаемый вывод:
        // ConcreteComponent operation.
        // Additional behavior.
    }
}

```

**Объяснение реализации:** Декоратор оборачивает оригинальный компонент, вызывая его метод и добавляя дополнительное поведение.

**Плюсы и минусы:**

Плюсы: гибкое расширение функционала, соблюдение принципа единой ответственности.

Минусы: может привести к большому количеству мелких классов, усложняя отладку.


</details>

<details>
  <summary><b>Адаптер (Adapter)</b></summary>

**Адаптер** — это структурный шаблон проектирования, который преобразует интерфейс одного класса в интерфейс, ожидаемый клиентом.

**Когда применять:** При необходимости интеграции классов с несовместимыми интерфейсами.

### 🔹 Пример реализации (C#)

```csharp
using System;

// Целевой интерфейс
public interface ITarget {
    void Request();
}

// Существующий класс с несовместимым интерфейсом
public class Adaptee {
    public void SpecificRequest() {
        Console.WriteLine("Specific request.");
    }
}

// Адаптер, преобразующий интерфейс
public class Adapter : ITarget {
    private Adaptee adaptee;
    public Adapter(Adaptee adaptee) {
        this.adaptee = adaptee;
    }
    public void Request() {
        adaptee.SpecificRequest();
    }
}

// Класс для демонстрации вызовов
public class Program {
    public static void Main() {
        Adaptee adaptee = new Adaptee();
        ITarget target = new Adapter(adaptee);
        target.Request(); // Ожидаемый вывод: Specific request.
    }
}
```
**Объяснение реализации:** Адаптер реализует целевой интерфейс, внутри вызывая методы адаптируемого класса, обеспечивая совместимость.

**Плюсы и минусы:**

Плюсы: позволяет повторно использовать существующий код, не изменяя его.

Минусы: добавляет дополнительный уровень абстракции.

</details>

<details>
  <summary><b>Фасад (Facade)</b></summary>

**Фасад** — это структурный шаблон проектирования, который предоставляет упрощённый интерфейс к сложной подсистеме.

**Когда применять:** Для упрощения работы с комплексными системами, скрывая детали реализации.

### 🔹 Пример реализации (C#)

```csharp
using System;

// Подсистема A
public class SubsystemA {
    public void OperationA() {
        Console.WriteLine("SubsystemA operation.");
    }
}

// Подсистема B
public class SubsystemB {
    public void OperationB() {
        Console.WriteLine("SubsystemB operation.");
    }
}

// Фасад, объединяющий операции подсистем
public class Facade {
    private SubsystemA subsystemA = new SubsystemA();
    private SubsystemB subsystemB = new SubsystemB();
    public void Operation() {
        subsystemA.OperationA();
        subsystemB.OperationB();
    }
}

// Класс для демонстрации вызовов
public class Program {
    public static void Main() {
        Facade facade = new Facade();
        facade.Operation();
        // Ожидаемый вывод:
        // SubsystemA operation.
        // SubsystemB operation.
    }
}
```
**Объяснение реализации:** Фасад инкапсулирует вызовы нескольких классов-подсистем, предоставляя единый метод для клиента.

**Плюсы и минусы:**

Плюсы: упрощение интерфейса, снижение связанности.

Минусы: может скрыть полезный функционал подсистем для опытных пользователей.

</details>

<details>
  <summary><b>Компоновщик (Composite)</b></summary>

**Компоновщик** — это структурный шаблон проектирования, который объединяет объекты в древовидные структуры для представления иерархий «часть-целое», позволяя работать с отдельными объектами и их группами единообразно.

**Когда применять:** Когда требуется представление сложных иерархий, где клиенту нужно работать с отдельными элементами и группами одинаково.
### 🔹 Пример реализации (C#)

```csharpusing System;
using System.Collections.Generic;

// Абстрактный компонент
public abstract class Component {
    public abstract void Operation();
}

// Лист – конечный элемент
public class Leaf : Component {
    public override void Operation() {
        Console.WriteLine("Leaf operation.");
    }
}

// Композит – контейнер компонентов
public class Composite : Component {
    private List<Component> children = new List<Component>();
    public void Add(Component component) {
        children.Add(component);
    }
    public void Remove(Component component) {
        children.Remove(component);
    }
    public override void Operation() {
        foreach (var child in children)
            child.Operation();
    }
}

// Класс для демонстрации вызовов
public class Program {
    public static void Main() {
        Composite root = new Composite();
        root.Add(new Leaf());
        
        Composite branch = new Composite();
        branch.Add(new Leaf());
        branch.Add(new Leaf());
        
        root.Add(branch);
        root.Operation();
        // Ожидаемый вывод: несколько строк "Leaf operation." в зависимости от иерархии.
    }
}
```
**Объяснение реализации:** Композит содержит коллекцию компонентов (листьев или других композитов) и делегирует им вызов операций, позволяя клиенту работать с иерархией как с единым объектом.

**Плюсы и минусы:**

Плюсы: единообразный интерфейс для всех элементов, гибкость в организации структуры.

Минусы: усложнение модели, если листья и композиты сильно различаются по функционалу.
</details>

<details>
  <summary><b>Заместитель (Proxy)</b></summary>

**Заместитель** — это структурный шаблон проектирования, который представляет собой объект-заместитель, контролирующий доступ к другому объекту.

**Когда применять:** Когда нужно управлять доступом, отложенной инициализацией или логированием вызовов к реальному объекту.

### 🔹 Пример реализации (C#)

```csharpusing System;

// Интерфейс субъекта
public interface ISubject {
    void Request();
}

// Реальный субъект
public class RealSubject : ISubject {
    public void Request() {
        Console.WriteLine("RealSubject request.");
    }
}

// Заместитель, контролирующий доступ
public class Proxy : ISubject {
    private RealSubject realSubject;
    public void Request() {
        if (realSubject == null)
            realSubject = new RealSubject();
        Console.WriteLine("Proxy controlling access.");
        realSubject.Request();
    }
}

// Класс для демонстрации вызовов
public class Program {
    public static void Main() {
        ISubject proxy = new Proxy();
        proxy.Request();
        // Ожидаемый вывод:
        // Proxy controlling access.
        // RealSubject request.
    }
}
```
**Объяснение реализации:** Класс Proxy реализует тот же интерфейс, что и реальный объект, и добавляет дополнительную логику (например, отложенную инициализацию).

**Плюсы и минусы:**

Плюсы: контроль доступа, возможность кэширования или логирования вызовов.

Минусы: дополнительный уровень абстракции, потенциальное снижение производительности.

</details>

<details>
  <summary><b>Мост (Bridge)</b></summary>

**Мост** — это структурный шаблон проектирования, который разделяет абстракцию и её реализацию, позволяя им развиваться независимо.

**Когда применять:** Когда необходимо разделить абстрактные и конкретные реализации, особенно если их независимое развитие возможно по двум осям.

### 🔹 Пример реализации (C#)

```csharp
using System;
// Интерфейс реализации
public interface IImplementor {
    void OperationImpl();
}

public class ConcreteImplementorA : IImplementor {
    public void OperationImpl() {
        Console.WriteLine("ConcreteImplementorA operation.");
    }
}

// Абстракция, использующая реализацию
public abstract class Abstraction {
    protected IImplementor implementor;
    public Abstraction(IImplementor implementor) {
        this.implementor = implementor;
    }
    public abstract void Operation();
}

public class RefinedAbstraction : Abstraction {
    public RefinedAbstraction(IImplementor implementor) : base(implementor) { }
    public override void Operation() {
        implementor.OperationImpl();
    }
}

// Класс для демонстрации вызовов
public class Program {
    public static void Main() {
        IImplementor implementor = new ConcreteImplementorA();
        Abstraction abstraction = new RefinedAbstraction(implementor);
        abstraction.Operation();
        // Ожидаемый вывод: ConcreteImplementorA operation.
    }
}
```
**Объяснение реализации:** Абстракция делегирует выполнение методов объекту-реализации. Это позволяет менять как абстракцию, так и реализацию независимо друг от друга.

**Плюсы и минусы:**

Плюсы: гибкость, снижение связности, независимое расширение обеих сторон.

Минусы: усложнение архитектуры, может быть избыточным для простых систем.

</details>

<details>
  <summary><b>Приспособленец (Flyweight)</b></summary>

**Приспособленец** — это структурный шаблон проектирования, который позволяет эффективно использовать память, разделяя общие данные между множеством мелких объектов.

**Когда применять:** Когда в системе требуется большое количество объектов, многие из которых имеют общие части состояния.

### 🔹 Пример реализации (C#)

```csharpusing System;
using System;
using System.Collections.Generic;

// Приспособленец с внутренним (общим) состоянием
public class Flyweight {
    private string intrinsicState;
    public Flyweight(string intrinsicState) {
        this.intrinsicState = intrinsicState;
    }
    public void Operation(string extrinsicState) {
        Console.WriteLine("Intrinsic: " + intrinsicState + ", Extrinsic: " + extrinsicState);
    }
}

// Фабрика приспособленцев
public class FlyweightFactory {
    private Dictionary<string, Flyweight> flyweights = new Dictionary<string, Flyweight>();
    public Flyweight GetFlyweight(string key) {
        if (!flyweights.ContainsKey(key))
            flyweights[key] = new Flyweight(key);
        return flyweights[key];
    }
}

// Класс для демонстрации вызовов
public class Program {
    public static void Main() {
        FlyweightFactory factory = new FlyweightFactory();
        Flyweight fly1 = factory.GetFlyweight("SharedState");
        fly1.Operation("Unique1");
        Flyweight fly2 = factory.GetFlyweight("SharedState");
        fly2.Operation("Unique2");
        // Ожидаемый вывод:
        // Intrinsic: SharedState, Extrinsic: Unique1
        // Intrinsic: SharedState, Extrinsic: Unique2
    }
}
```
**Объяснение реализации:** Фабрика создаёт или возвращает уже существующий объект с нужным внутренним состоянием. Внешнее состояние передаётся методам объекта, позволяя разделять данные.

**Плюсы и минусы:**

Плюсы: значительное сокращение потребления памяти, особенно при большом количестве объектов.

Минусы: усложнение логики за счёт разделения состояния, повышенная зависимость от корректного разделения внутреннего и внешнего состояния.

</details>

### Ссылки на литературу
<details><summary>Ссылки</summary>  
Ссылки на литературу которая была использоана при написании данного конспекта:  

- [Метанит.com — Руководство по C#](https://metanit.com/sharp/tutorial/)
- [Вопросы для подготовки к собеседованию по C#](https://github.com/vadsemenov/CSharp-job-questions?tab=readme-ov-file#------------------------------------------c-------------net--------------------------------------------junior-middle)
- [Делегаты и Лямбда выражения в C#](https://habr.com/ru/articles/329886/)
- [Документация по C#](https://professorweb.ru/my/csharp/charp_theory/level1/infocsharp.php)
- [Паттерны C#](https://github.com/stacenko-developer/Patterns?tab=readme-ov-file#Структурные-паттерны)
</details>

