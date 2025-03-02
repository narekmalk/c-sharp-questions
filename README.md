<div align="center">
  <img height="120" src="https://narekmalk.com/images/csharp.png">
  <h1>Tricky C# Questions & Answers</h1>
  <p>Test your C# knowledge before an interview with these questions of type "what's the output of the following code snippet". In many cases you'll find answers surprising. Please leave a star.</p>
</div>

---

###### <img align="center" height="40" src="https://narekmalk.com/images/question.png"> &nbsp; 1. What's the output?

```cs
class Foo<T>
{
    public static int Bar;
}

void Main()
{
    Foo<int>.Bar++;
    Console.WriteLine(Foo<double>.Bar);
}
```

<details><summary><b>Answer</b></summary>
<p>

#### Output: 
0

#### Explanation: 
`Foo<int>` and `Foo<double>` are considered two different types due to the generic parameter. So, the `Bar` of `Foo<int>` is different from `Bar` of `Foo<double>`.

</p>
</details>

---

###### <img align="center" height="40" src="https://narekmalk.com/images/question.png"> &nbsp; 2. What's the output?

```cs
static void Main(string[] args)
{
    Console.WriteLine(Math.Round(6.5));
    Console.WriteLine(Math.Round(11.5));
}
```

<details><summary><b>Answer</b></summary>
<p>

#### Output: 
6<br/>
12
#### Explanation: 
.NET uses "Banker's Rounding" (also known as "Round Half to Even") as the default rounding mechanism. In this method, if the number to be rounded is exactly halfway between two other numbers, it is rounded to the nearest even number. This method is often used in financial calculations to reduce bias.

</p>
</details>

---

###### <img align="center" height="40" src="https://narekmalk.com/images/question.png"> &nbsp; 3. What's the output?

```cs
Console.WriteLine(1 + 2 + 'A');
Console.WriteLine(1 + 'A' + 2);
Console.WriteLine('A' + 1 + 2);
```

<details><summary><b>Answer</b></summary>
<p>

#### Output: 
68  
68  
68

#### Explanation: 
When adding types `Int32` and `Char`, conversion of `Char` to `Int32` happens. Thus, in all 3 cases result will be the code of symbol `'A'` (65) increased by 3.

</p>
</details>

---

###### <img align="center" height="40" src="https://narekmalk.com/images/question.png"> &nbsp; 4. What's the output?

```cs
static String str;
static DateTime time;

static void Main(string[] args)
{
    Console.WriteLine(str == null ? "str == null" : str);
    Console.WriteLine(time == null ? "time == null" : time.ToString());
}
```

<details><summary><b>Answer</b></summary>
<p>

#### Output: 
str == null <br/>
1/1/0001 12:00:00 AM
#### Explanation: 
Both variables are not initialized, but a string is a reference type and DateTime is a value type. The default value of DateTime type is DateTime.MinValue, which equals 1/1/0001 12:00:00 AM.

</p>
</details>


---

###### <img align="center" height="40" src="https://narekmalk.com/images/question.png"> &nbsp; 5. What's the output?

```cs
var bar = new Bar { Foo = new Foo() };
bar.Foo.Change(5);
Console.WriteLine(bar.Foo.Value);

public struct Foo
{
    public int Value;
    public void Change(int newValue)
    {
        Value = newValue;
    }
}
public class Bar
{
    public Foo Foo { get; set; }
}
```

<details><summary><b>Answer</b></summary>
<p>

#### Output: 
0

#### Explanation: 
Structs are copied by value, not by reference. When we refer to property `bar.Foo`, the method `bar.get_Foo()` is called, which returns us the copy of the structure, thus, the original structure remains unchanged. Then, when calling `WriteLine`, we again refer to the same property and are printing `Value` of a new copy of `Foo`, which is 0.

</p>
</details>

---

###### <img align="center" height="40" src="https://narekmalk.com/images/question.png"> &nbsp; 6. What's the output?

```cs
foreach (Foo current in Baz().ToList())
{
    Console.WriteLine(current.Bar);
}
Console.WriteLine("--delimiter--");
foreach (Foo current in Baz())
{
    Console.WriteLine(current.Bar);
}

IEnumerable<Foo> Baz() 
{
    Foo instance = new Foo();
  
    for (int i=0; i<10; i++)
    {
        instance.Bar++;
        yield return instance;
    }
}

class Foo 
{
    public int Bar {get; set;}
}
```

<details><summary><b>Answer</b></summary>
<p>

#### Output: 
10<br/>
10<br/>
10<br/>
10<br/>
10<br/>
10<br/>
10<br/>
10<br/>
10<br/>
10<br/>
--delimiter--<br/>
1<br/>
2<br/>
3<br/>
4<br/>
5<br/>
6<br/>
7<br/>
8<br/>
9<br/>
10<br/>
#### Explanation: 
In the first loop we turn `IEnumerable` to `List`, so we end up with a list of references to the same object. In the second loop we print the value of `Bar` as we iterate over the `IEnumerable`.

</p>
</details>




---

###### <img align="center" height="40" src="https://narekmalk.com/images/question.png"> &nbsp; 7. What's the output?

```cs
var list = new List<string> { "Foo", "Bar", "Baz" };
var startLetter = "F";
var query = list.Where(c => c.StartsWith(startLetter));
startLetter = "B";
query = query.Where(c => c.StartsWith(startLetter));
Console.WriteLine(query.Count());
```

<details><summary><b>Answer</b></summary>
<p>

#### Output: 
2

#### Explanation: 
Because of deferred execution, queries are executed only at the point `query.Count()` is called. At this point, both filters are applied with `startLetter` set to "B".

</p>
</details>


---

###### <img align="center" height="40" src="https://narekmalk.com/images/question.png"> &nbsp; 8. What's the output?

```cs
class A
{
    public void Abc(int q)
    {
        Console.WriteLine("Abc from A");
    }
}

class B : A
{
    public void Abc(double p)
    {
        Console.WriteLine("Abc from B");
    }
}

static void Main(string[] args)
{
    int i = 5;
    B b = new B();
    b.Abc(i);
}
```

<details><summary><b>Answer</b></summary>
<p>

#### Output: 
Abc from B
#### Explanation: 
Contrary to Java, in C# a class is defined as a component that attempts to be self-sufficient whenever possible. So, the compiler first is looking at the class itself and attempts to resolve a symbol that is requested.

</p>
</details>

---

###### <img align="center" height="40" src="https://narekmalk.com/images/question.png"> &nbsp; 9. What's the output?

```cs
delegate void SomeMethod();

static void Main(string[] args)
{
    List<SomeMethod> delList = new List<SomeMethod>();
    for (int i = 0; i < 10; i++)
    {
        delList.Add(delegate { Console.WriteLine(i); });
    }

    foreach (var del in delList)
    {
        del();
    }
}
```

<details><summary><b>Answer</b></summary>
<p>

#### Output: 
10  
10  
10  
10  
10  
10  
10  
10  
10  
10

#### Explanation: 
The tricky part here is understanding closures in C#. When the delegate is created, a closure is created, which captures the variable i by reference, not by value. This means that when the delegate is invoked, it will use the value of i at the time of invocation (which is 10), not the value of i at the time the delegate was created. If you wanted each delegate to remember the value of i at the time it was created, you would need to create a temporary variable inside the loop, assign i to it, and use that in the delegate.

</p>
</details>


---

###### <img align="center" height="40" src="https://narekmalk.com/images/question.png"> &nbsp; 10. What's the output?

```cs
static void Main(string[] args)
{
    string hello = "hello";
    string helloWorld = "hello world";
    string helloWorld2 = "hello world";
    string helloWorld3 = hello + " world";

    Console.WriteLine(helloWorld == helloWorld2);
    Console.WriteLine(object.ReferenceEquals(helloWorld, helloWorld2));
    Console.WriteLine(object.ReferenceEquals(helloWorld, helloWorld3));
}
```

<details><summary><b>Answer</b></summary>
<p>

#### Output: 
True  
True  
False

#### Explanation: 
1. This line checks if the values of helloWorld and helloWorld2 are equal.
2. This line checks if helloWorld and helloWorld2 refer to the exact same object. In C#, the .NET runtime performs a process called string interning for literal strings. This means that when you have two or more identical string literals in your code, the runtime only creates one string object, and all variables that are assigned that string literal actually refer to the same object.
3. In this line, helloWorld3 is created by concatenating hello and " world", which creates a new string object. So even though the value of helloWorld3 is also "hello world", it's not the same object as helloWorld.

</p>
</details>

---

###### <img align="center" height="40" src="https://narekmalk.com/images/question.png"> &nbsp; 11. What's the output?

```cs
public class TestStatic {
    public static int TestValue;

    public TestStatic() {
        if (TestValue == 0) {
            TestValue = 5;
        }
    }
    static TestStatic() {
        if (TestValue == 0) {
            TestValue = 10;
        }
    }

    public void Print() {
        if (TestValue == 5) {
            TestValue = 6;
        }

        Console.WriteLine("TestValue : " + TestValue);
    }
}

public void Main(string[] args) {
    TestStatic t = new TestStatic();
    t.Print();
}
```

<details><summary><b>Answer</b></summary>
<p>

#### Output: 
TestValue : 10

#### Explanation: 
In C#, a static constructor (also called a type initializer) is called automatically before the first instance is created or any static members are referenced. During the execution of the static constructor, TestValue is 0, so it is set to 10. After that, the instance constructor is run, and than t.Print() is called, but these methods don't change TestValue.

</p>
</details>

---

###### <img align="center" height="40" src="https://narekmalk.com/images/question.png"> &nbsp; 12. What's the output?

```cs
using System.Threading.Tasks;

public static void Main(string[] args)
{
    Console.WriteLine("Main start");
    Method1();
    Console.WriteLine("Main end");
    Console.ReadLine();
}

public static async void Method1()
{
    Console.WriteLine("Method1 start");
    await Method2();
    Console.WriteLine("Method1 end");
}

public static async Task Method2()
{
    Console.WriteLine("Method2 start");
    await Task.Delay(1000);
    Console.WriteLine("Method2 end");
}
```

<details><summary><b>Answer</b></summary>
<p>

#### Output: 
Main start  
Method1 start  
Method2 start  
Main end  
Method2 end  
Method1 end

#### Explanation: 
The Main method prints "Main start".  
Next, Method1() is called. This is an async method which starts by printing "Method1 start".  
Method1() then calls Method2() using await, meaning it will asynchronously wait for Method2() to complete before it continues. Method2() is an async method that returns a Task. It starts by printing "Method2 start".  
Inside Method2(), we call await Task.Delay(1000). This will pause Method2() for 1 second, during which control is returned back to the calling method.  
Since we are awaiting Method2() in Method1(), control is returned back to the Main method. The "Main end" message is printed.  
The Console.ReadLine() at the end of Main method keeps the program running, which allows us to see the delayed output from the other methods.  
After the delay in Method2(), it prints "Method2 end" and completes.  
Since Method1() was awaiting Method2(), after Method2() completes, control is returned back to Method1() which then prints "Method1 end" and completes.

</p>
</details>



---

###### <img align="center" height="40" src="https://narekmalk.com/images/question.png"> &nbsp; 13. What's the output?

```cs
using System;
using System.Reflection;

public class Example
{
    public readonly int ReadOnlyField;

    public Example(int value)
    {
        ReadOnlyField = value;
    }
}

public class Program
{
    public static void Main(string[] args)
    {
        Example example = new Example(10);
        Console.WriteLine($"Before applying reflection: {example.ReadOnlyField}");

        // Applying reflection to change the value of readonly field
        var field = typeof(Example).GetField("ReadOnlyField");
        field.SetValue(example, 20);

        Console.WriteLine($"After applying reflection: {example.ReadOnlyField}");
    }
}
```

<details><summary><b>Answer</b></summary>
<p>

#### Output: 
Before applying reflection: 10  
After applying reflection: 20

#### Explanation: 
It's possible to use Reflection to change the value of a `readonly` field, though doing so can lead to unexpected behavior and is generally not recommended as it violates the principle of immutability that `readonly` keyword is meant to enforce.

</p>
</details>

---

###### <img align="center" height="40" src="https://narekmalk.com/images/question.png"> &nbsp; 14. What's the output?

```cs
var s = new S();

using (s)
{
    Console.WriteLine(s.GetDispose());
}
Console.WriteLine(s.GetDispose());

public struct S : IDisposable
{
    private bool dispose;
    public void Dispose()
    {
        dispose = true;
    }
    public bool GetDispose()
    {
        return dispose;
    }
}
```

<details><summary><b>Answer</b></summary>
<p>

#### Output: 
False  
False

#### Explanation: 
`using` makes a copy of the value type, and you are therefore disposing a copy, not the original. More details: https://ericlippert.com/2011/03/14/to-box-or-not-to-box/

</p>
</details>

---

###### <img align="center" height="40" src="https://narekmalk.com/images/question.png"> &nbsp; 15. What's the output?

```cs
class Program
{
    private static Object syncObject = new Object();
    private static void Write()
    {
        lock (syncObject)
        {
            Console.WriteLine("test");
        }
    }
    static void Main(string[] args)
    {
        lock (syncObject)
        {
            Write();
        }
    }
}
```

<details><summary><b>Answer</b></summary>
<p>

#### Output: 
test  

#### Explanation: 
The `Write` method attempts to acquire a lock on the same `syncObject`. Normally, this could be a problem—if another thread were involved, it would result in a deadlock because the `Main` method already holds the lock. However, in this case, since there are no multiple threads involved, the lock is re-entrant. A re-entrant lock means that the same thread can acquire the same lock multiple times without causing a deadlock. It already holds the lock, so it is allowed to proceed.

</p>
</details>

---

###### <img align="center" height="40" src="https://narekmalk.com/images/question.png"> &nbsp; 16. What's the output?

```cs
int a = 0;
int Foo()
{
    a = a + 42;
    return 1;
}
void Main()
{
    a += Foo();
    Console.WriteLine(a);
}
```

<details><summary><b>Answer</b></summary>
<p>

#### Output: 
1  

#### Explanation: 
`a += Foo()` will be converted to `a = a + Foo()`. Firstly, left operand will be evaluated, which is 0, then, right operand will be evaluated, which returns 1, so the result will be 1, despite the fact that `a` is reassigned inside `Foo()`.

</p>
</details>

---

###### <img align="center" height="40" src="https://narekmalk.com/images/question.png"> &nbsp; 17. What's the output?

```cs
static void Main(string[] args)
{
    object sync = new object();
    var thread = new Thread(()=>
    {
        try
        {
            Work();
        }
        finally
        {
            lock (sync)
            {
                Monitor.PulseAll(sync);
            }
        }
    });
    thread.Start();
    lock (sync)
    {
        Monitor.Wait(sync);
    }
    Console.WriteLine("test");
}
private static void Work()
{
    Thread.Sleep(1000);
}
```

<details><summary><b>Answer</b></summary>
<p>

#### Output: 
test

#### Explanation: 
When calling `Monitor.Wait(sync)`, `sync` object is released before waiting for pulsing. Therefore, the thread is able to enter `lock` block and call `Monitor.PulseAll(sync)`, which awakens the main thread.

</p>
</details>

---

###### <img align="center" height="40" src="https://narekmalk.com/images/question.png"> &nbsp; 18. What's the output?

```cs
void Foo(object a)
{
    Console.WriteLine("object");
}
void Foo(object a, object b)
{
    Console.WriteLine("object, object");
}
void Foo(params object[] args)
{
    Console.WriteLine("params object[]");
}
void Foo<T>(params T[] args)
{
    Console.WriteLine("params T[]");
}
class Bar { }
void Main()
{
    Foo();
    Foo(null);
    Foo(new Bar());
    Foo(new Bar(), new Bar());
    Foo(new Bar(), new object());
}
```

<details><summary><b>Answer</b></summary>
<p>

#### Output: 
params object[]  
params object[]  
params T[]  
params T[]  
object, object

#### Explanation: 
Let's look at each case.

`Foo()` -> `params object[]`  
Versions `object, object`, `object` are not suitable because of number of arguments. Version `params T[]` is not suitable, because `T` can't be resolved. Thus, correct version is `params object[]`.

`Foo(null)` -> `params object[]`  
Version `object, object` is not suitable because of number of arguments. Version `params T[]` is not suitable, because `T` can't be resolved. From the two remaining versions compiler will choose `params object[]` - I don't know why :) 

`Foo(new Bar())` -> `params T[]`  
Version `object, object` is not suitable because of number of arguments. Versions `object` and `params object[]` will require additional cast of `Bar` to `object`, thus, `params T[]` is more preferrable.

`Foo(new Bar(), new Bar())` -> `params T[]`  
Version `object` is not suitable because of number of arguments. Versions `object, object` and `params object[]` will require additional cast of `Bar` to `object`, thus, `params T[]` is more preferrable.

`Foo(new Bar(), new object())` -> `object, object`  
Version `object` is not suitable because of number of arguments. Among the remaining versions `object, object` is the most specific one.

</p>
</details>

---

###### <img align="center" height="40" src="https://narekmalk.com/images/question.png"> &nbsp; 19. What's the output?

```cs
IEnumerable<string> Foo()
{
    yield return "Bar";
    Console.WriteLine("Baz");
}
void Main()
{
    foreach (var str in Foo())
        Console.WriteLine(str);
}
```

<details><summary><b>Answer</b></summary>
<p>

#### Output: 
Bar  
Baz

#### Explanation: 
First iteration of foreach `yield return`s "Bar" which is written to console. Second iteration tries to find another `yield return` (meanwhile writing to console "Baz") but finds nothing and the loop ends.

</p>
</details>

---

###### <img align="center" height="40" src="https://narekmalk.com/images/question.png"> &nbsp; 20. What's the output?

```cs
var x = "AB";
var y = new System.Text.StringBuilder().Append('A').Append('B').ToString();
var z = string.Intern(y);
Console.WriteLine(x == y);
Console.WriteLine(x == z);
Console.WriteLine((object)x == (object)y);
Console.WriteLine((object)x == (object)z);
```

<details><summary><b>Answer</b></summary>
<p>

#### Output: 
True  
True  
False  
True

#### Explanation: 
First two will print `True`, because we are comparing by value. Next two are comparing by reference. `x` points to interned string `"AB"` as it's declared with string literal. `z` points to the same interned string as it's defined with method `string.Intern`. But `y` will point to other memory location as it's defined with `StringBuilder`, which doesn't consider interned strings when calling `ToString()`.

</p>
</details>

---

###### <img align="center" height="40" src="https://narekmalk.com/images/question.png"> &nbsp; 21. What's the output?

```cs
try
{
    Console.WriteLine(((string)null + null + null) == "");
}
catch (Exception e)
{
    Console.WriteLine(e.GetType());
}
```

<details><summary><b>Answer</b></summary>
<p>

#### Output: 
True

#### Explanation: 
If an operand of string concatenation is null, an empty string is substituted.

</p>
</details>

---

<br>
<br>


### Sources
* Own experience
* https://github.com/AndreyAkinshin/ProblemBook.NET
* https://metanit.com/sharp/interview
