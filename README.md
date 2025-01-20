# 15.Collections
Nous avons déjà vu précédemment quelques petites notions sur les listes. Dans ce chapitre, on va s'attaquer complètement aux listes. 

## 0. arrays
Arrays are one of the most basic data structures in C#. They provide a way to store a fixed-size collection of elements of the same type. Here’s a quick refresher on how to declare, initialize, and access arrays:

```csharp
// Declaring an array of integers with 5 elements
int[] numbers = new int[5];
numbers[0] = 1;
numbers[1] = 2;
numbers[2] = 3;
numbers[3] = 4;

var theDefaultValue = numbers[4]; //0
var notPossible = numbers[5]; //throws an IndexOutOfRangeException

// Initializing an array with values
int[] numbers = { 1, 2, 3, 4, 5 };
```

## 1. IEnumerable<T>
The IEnumerable<T> interface is essential in .NET as it enables iteration over a collection of items of type T. Classes and interfaces that represent generic collections, like lists or arrays, implement this interface.

To understand the use of **yield** and **lazy loading**, consider an example where we want to return a series of numbers without storing all of them in memory at once. This is particularly useful for managing large data sets or resource-intensive operations.

```csharp 
using System;
using System.Collections.Generic;

class Program
{
    static void Main()
    {
        foreach (int number in GetNumbers())
        {
            Console.WriteLine(number);
        }
    }

    // Using yield to return a sequence of numbers
    public static IEnumerable<int> GetNumbers()
    {
        for (int i = 0; i < 10; i++)
        {
            // Here, the 'yield' keyword allows returning one element at a time
            // each iteration of the for loop is lazily returned upon the iterator's call
            yield return i;
        }
    }
}
```

In this example, `GetNumbers` generates a sequence of numbers from 0 to 9. The `yield` keyword returns each element one at a time to the iterator (`foreach` in `Main`). This means that the elements are generated one by one on demand, which is a form of lazy loading since the entire collection is never stored in memory.

This example illustrates how `IEnumerable<T>`, combined with `yield`, facilitates efficient and resource-saving management of collections.

## 2. Lists 
In C#, `List<T>` is a generic collection type that provides a flexible way to store a dynamically-sized list of elements of a specific type (`T`). Unlike arrays, which have a fixed size, lists can grow and shrink as needed, making them a powerful tool for managing collections of items in a more dynamic way.

**Key Characteristics of List<T>**

- **Dynamically Sized**: Lists automatically adjust their size as elements are added or removed, so you don’t need to specify the size ahead of time.

- **Type Safety**: `List<T>` is generic, meaning it holds elements of a specific type (`T`), ensuring type safety. For example, `List<int>` can only contain integers, while `List<string>` can only contain strings.

- **Easy Access to Elements**: Like arrays, lists allow quick access to elements by index, starting from `0` for the first element.

**Basic Operations with List<T>:**

```csharp 
List<int> numbers = new List<int> { 1, 2, 3, 4, 5 };
List<int> numbers = [1, 2, 3, 4, 5];
```

### 1. Methods for lists
- Add / AddRange :
    - **Add()**: Add a single item at the end of the list 
    - **AddRange()**: Add multiply items 
```csharp 
List<int> numbers = new List<int> {1,2,3};
numbers.AddRange(new int[] {4,5,6})
```

- Remove / RemoveAt :
    - **Remove()**: Remove the first occurence of a specific element 
    - **RemoveAt()**: Removes an element at the specified index

```csharp 
List<Int> numbers = new List<int> {1,2,3};
numbers.Remove(2) // It removes the 2 number
numbers.RemoveAt(2) // It removes the number of index 2, so it will be 3.
```

- Insert: 
    - **Insert**: Add an item at a specific index 

```csharp 
List<Int> numbers = new List<int> {1,2,3};
numbers.Insert(3,10) // Add 10 at index 3
```

- IndexOf :
    - **IndexOf**: Returns the first occurence of the given index

```csharp 
List<Int> numbers = new List<int> {1,2,3};
Console.Writeline(numbers.IndexOf(1)) // it will be 0
```

- Count :
    - **Count**: Returns the number of element in the list 

```csharp 
List<Int> numbers = new List<int> {1,2,3};
Console.Writeline(numbers.Count()) // 3
```

- Sort : 
    - **Sort**:  Sorts the elements in the list in ascending order

```csharp 
List<Int> numbers = new List<int> {1,3,2};
numbers.Sort() // 1,2,3
```

- Reverse: 
    - **Reverse**: Reverses the order of elements in the list

```csharp 
List<Int> numbers = new List<int> {1,3,2};
numbers.Reverse() // 2,3,1
```

## 3. Other amazing generic collection types

- `Array<T>`
- `Dictionary<TKey, TValue>`
- `HashSet<T>`
- `ImmutableArray<T>`
- `Queue<T>`
- `Stack<T>`

### 1. Dictionary
A `Dictionary<TKey, TValue>` is a collection that maps keys to values, where both keys and values have specific types. It uses a hash code for fast lookups.

```csharp 
Dictionary<string,int> dictionnary = new Dictionary<string,int>();
dictionnary["one"] = 1

Dictionary<int,User> users = new Dictionary<int,User>();
users[0] = new User{firstname = "Pierre", lastname = "John"}
```

Refer to the official documentation to learn more about the methods available in dictionaries.

### 2. HashSet 
A `HashSet<T>` is a collection that stores a set of values. It also uses a hash code for fast lookups and does not allow duplicate values.

```csharp 
HashSet<int> hashSet = new HashSet<int>();
hashSet.Add(1);
hashSet.Add(2);
hashSet.Add(2); // This will not be added because it is a duplicate 
``` 

### 3. ImmutableArray<T>
An `ImmutableArray<T>` is a collection that maintains a fixed-size array of elements. It is immutable, which means that its size and contents cannot be altered once established.

```csharp 
ImmutableArray<int> immutableArray = ImmutableArray.Create(1, 2, 3, 4, 5);
```

When adding to the array, the operation yields a new `ImmutableArray<T>` that includes the additional element.

```csharp 
ImmutableArray<int> newImmutableArray = immutableArray.Add(6);
```

### 4. Queue<T> and Stack<T>

A `Queue<T>` manages elements in a first-in, first-out (FIFO) sequence.

```csharp 
Queue<int> queue = new Queue<int>();
queue.Enqueue(1);
queue.Enqueue(2);
queue.Enqueue(3);

int first = queue.Dequeue(); // 1
int second = queue.Dequeue(); // 2
```

Conversely, a `Stack<T>` handles elements in a last-in, first-out (LIFO) order.

```csharp 
Stack<int> stack = new Stack<int>();
stack.Push(1);
stack.Push(2);
stack.Push(3);

int top = stack.Pop(); // 3
int second = stack.Pop(); // 2
int first = stack.Pop(); // 1
```

Although not frequently employed, both Stack<T> and Queue<T> have specific uses in various programming scenarios.

## 4. Exercices