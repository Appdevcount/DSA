Got it ✅ — you’re starting **Data Structures & Algorithms (DSA)** in C#, so you want to get comfortable with the C# logic, syntax, and built-in features you’ll actually use while solving problems.

I’ll give you a **C# DSA Quick Syntax Guide** — so you won’t get stuck on the language while focusing on algorithms.

---

## **1. Variables & Data Types**

```csharp
int num = 10;             // Integer
double pi = 3.14;         // Decimal number
char letter = 'A';        // Single character
string name = "Siraj";    // String
bool isValid = true;      // Boolean
```

---

## **2. Arrays**

```csharp
int[] arr = { 1, 2, 3, 4 };
Console.WriteLine(arr[0]);   // Access element
arr[2] = 10;                  // Modify element
Console.WriteLine(arr.Length); // Length
```

---

## **3. Strings (Important for DSA problems)**

```csharp
string s = "hello";
Console.WriteLine(s[0]);        // Access like array -> 'h'
Console.WriteLine(s.Length);    // Length
string sub = s.Substring(1, 3); // "ell"
string upper = s.ToUpper();     // "HELLO"
bool contains = s.Contains("lo"); // true
```

---

## **4. Lists (`List<T>`)**

```csharp
List<int> nums = new List<int> { 1, 2, 3 };
nums.Add(4);          // Add element
nums.Remove(2);       // Remove element
nums.Insert(1, 10);   // Insert at index
Console.WriteLine(nums[1]); // Index access
Console.WriteLine(nums.Count); // Count
```

---

## **5. Loops**

```csharp
// For loop
for (int i = 0; i < arr.Length; i++)
    Console.WriteLine(arr[i]);

// Foreach loop
foreach (int n in arr)
    Console.WriteLine(n);

// While loop
int x = 0;
while (x < 5)
    x++;
```

---

## **6. Conditions**

```csharp
int n = 5;
if (n > 0)
    Console.WriteLine("Positive");
else if (n == 0)
    Console.WriteLine("Zero");
else
    Console.WriteLine("Negative");
```

---

## **7. Functions**

```csharp
int Sum(int a, int b)
{
    return a + b;
}
Console.WriteLine(Sum(3, 4)); // 7
```

---

## **8. Dictionary (HashMap)**

```csharp
Dictionary<string, int> map = new Dictionary<string, int>();
map["apple"] = 2;
map["banana"] = 5;

Console.WriteLine(map["apple"]);      // 2
Console.WriteLine(map.ContainsKey("banana")); // true
```

---

## **9. Queue & Stack (Important for BFS/DFS)**

```csharp
// Queue (FIFO)
Queue<int> q = new Queue<int>();
q.Enqueue(1);
q.Enqueue(2);
Console.WriteLine(q.Dequeue()); // 1

// Stack (LIFO)
Stack<int> st = new Stack<int>();
st.Push(10);
st.Push(20);
Console.WriteLine(st.Pop());    // 20
```

---

## **10. LINQ (Useful for Quick Operations)**

```csharp
int[] numbers = { 1, 2, 3, 4 };
var evenNumbers = numbers.Where(n => n % 2 == 0);
Console.WriteLine(string.Join(", ", evenNumbers)); // 2, 4
```

---

💡 **My Advice for DSA in C#:**

* Focus on **`string`**, **`List<T>`**, **`Dictionary<T, T>`**, **`Queue<T>`**, **`Stack<T>`**, and loops — 80% of problems will use these.
* Practice problems on **arrays, strings, and hash maps first**.
* Always watch for **off-by-one errors** with indexes (`0`-based indexing).

---

If you want, I can make you a **"DSA in C# Cheat Sheet"** with all syntax and patterns you'll keep reusing for arrays, strings, and collections so you never have to think about syntax while solving.
Do you want me to prepare that?
