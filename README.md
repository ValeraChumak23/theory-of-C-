## Конспект по языку программирования C# (платформа .NET)
- [Содержание](#содержание)
  - [Введение в C#](#введение-в-c)
  - [Основы программирования](#основы-программирования)
  - [ООП и все что с ним связано](#ооп-и-все-что-с-ним-связано)
  - [Обобщения](#обобщения)
  - [Делегаты](#делегаты)
  - [Интерфейсы](#интерфейсы)
  - [Паттерны](#паттерны)
  - [Коллекции](#коллекции)
  - [Ссылки на литературу](#литература)

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

### Ссылки на литературу
<details><summary>Ссылки</summary>  
Ссылки на литературу которая была использоана при написании данного конспекта:  

- [Метанит.com — Руководство по C#](https://metanit.com/sharp/tutorial/)
- [Вопросы для подготовки к собеседованию по C#](https://github.com/vadsemenov/CSharp-job-questions?tab=readme-ov-file#------------------------------------------c-------------net--------------------------------------------junior-middle)
- [Делегаты и Лямбда выражения в C#](https://habr.com/ru/articles/329886/)
</details>

