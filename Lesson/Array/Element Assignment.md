```java
int[] x = new int[5];
    x[0] = 10;

    x[1] = 'a';     // ❌❌ Compilation Error

    byte b = 20;
    x[2] = b;       // ✅ Implicit type conversion (byte -> int)

    short s = 30;
    x[3] = s;       // ✅ Implicit type conversion (short -> int)
    
    x[4] = 10L;     // ❌❌ Compilation Error
                    // CE: Possible Loss of Precision (PLP)
                    // Found: long
                    // Required: int
```

# Java Array Type Rules

## Case 1: Primitive Type Arrays

In the case of **primitive type arrays**, as array elements, we can provide any type that can be implicitly promoted to the declared type.

```java
Object[] a = new Object[10];
a[0] = new Object();
a[1] = new String("Aman");
a[2] = new Integer(10);
```

## Case 2: Object Type Arrays

In the case of **object type arrays**, as array elements, we can provide either declared type objects or child class objects.

```java
Number[] n = new Number[10];
n[0] = new Integer(10);        // ✅✅ Allowed (Integer is a subclass of Number)
n[1] = new Double(10.5);       // ✅✅ Allowed (Double is a subclass of Number)
n[2] = new String("Aman");    // ❌❌ Compilation Error
                                // CE: Incompatible types
                                // Found: java.lang.String
                                // Required: java.lang.Number
```

**Note:**

In the case of **float type arrays**, the allowed data types are `byte`, `short`, `char`, `int`, `long`, and `float`.

---

## Case 3: Interface Type Arrays

For **interface type arrays**, as array elements, its implementation class objects are allowed.

```java
Runnable[] r = new Runnable[10];
r[0] = new Thread();        // ✅✅ Allowed (Thread implements Runnable)
r[1] = new String("Aman"); // ❌❌ Compilation Error
                            // CE: Incompatible type
                            // Found: java.lang.String
                            // Required: java.lang.Runnable
```


| Array Type              | Allowed Element Type                                      |
|-------------------------|---------------------------------------------------------|
| **Primitive Type**      | Any type that can be implicitly promoted to declared type |
| **Object Type Arrays**  | Either the declared type or its child class objects      |
| **Abstract Class Type Arrays** | Only its child class objects                        |
| **Interface Type Arrays** | Objects of its implementation classes                   |



# **Array Variable Assignment**  

### **Example in Java:**  

```java
int[] x = {10, 20, 30, 40};  
char[] ch = {'a', 'b', 'c', 'd'};  

int[] b = x;  
int[] c = ch;  // ❌ Compilation Error  
               // CE: Incompatible types  
               // Found: char[]  
               // Required: int[]  
```

## **Note:**  
- ✅ If you assign an `int` value to a `char` variable, it **works fine**.  
- ❌ However, assigning an `int[]` array to a `char[]` array (or vice versa) results in a **Type Mismatch Compilation Error**.  

---

## **Case 1: Element-Level Promotion vs. Array-Level Promotion**  

✅ **Element-level promotion** is **possible**.  
❌ **Array-level promotion** is **not possible**.  

### **Example:**  

✅ A `char` element **can** be promoted to an `int` type.  
```java
char ch = 'A';  
int num = ch;  // ✅ Works fine  
System.out.println(num);  // Output: 65  
```

❌ A char[] array cannot be promoted to an int[] array.

```java
char[] charArray = {'A', 'B', 'C'};  
int[] intArray = charArray;  // ❌ Compilation Error  
```


## **Which of the following promotions will be performed automatically?**  

| **Expression**        | **Automatic Promotion** |
|----------------------|----------------------|
| `char → int`        | ✅ Yes              |
| `char[] → int[]`    | ❌ No               |
| `int → double`      | ✅ Yes              |
| `int[] → double[]`  | ❌ No               |
| `float → int`       | ❌ No               |
| `float[] → int[]`   | ❌ No               |
| `String → Object`   | ✅ Yes              |
| `String[] → Object[]` | ✅ Yes          |


## **Object Type Array Promotion**  

- ✅ In the case of **object type arrays**, a **child class type array** can be **promoted** to a **parent class type array**.  

---

## **Case 2: Array Assignment Behavior**  

- Whenever we assign **one array to another**, the **internal elements are not copied**.  
- Instead, the **reference variable** is **reassigned** to the new array.  

### **Example:**  
```java
int[] a = {1, 2, 3, 4, 5};  
int[] b = {6, 7, 8};  

a = b;  // ✅ Allowed  
b = a;  // ✅ Allowed  
 ```
![Array Reference Reassignment](./../../Images/Screenshot%202025-03-31%20114818.png)

## **Case 3: Matching Array Dimensions**  

- ✅ When assigning **one array to another**, the **dimensions must match**.  
- ❌ If we try to assign an array of a **different dimension**, we will get a **Compilation Error (CTE)**.  
- ✅ In a **1D array position**, we should provide a **1D array only**.  
- ✅ Multi-dimensional array assignments must follow strict type rules.

---

### **Example:**  

```java
int[][] a = new int[3][];  

a[0] = new int[4][3];  // ❌ Compilation Error  
                        // CE: Incompatible types  
                        // Found: int[][]  
                        // Required: int[]  

a[0] = 10;             // ❌ Compilation Error  
                        // CE: Incompatible types  
                        // Found: int  
                        // Required: int[]  

a[0] = new int[2];     // ✅ Allowed (Matching Dimensions)  
```

## **Note:**  
- ✅ When assigning **one array to another**, **both dimensions and types must match**.  
- ❌ However, **sizes do not need to match**.  

---

## **Understanding Object Creation & Garbage Collection in Java**  

### **Code:**
```java
int[][] a = new int[4][3];  // (Step 1) Creates 1 object -> 5  
a[0] = new int[4];          // (Step 2) Creates 1 object -> 1  
a[1] = new int[2];          // (Step 3) Creates 1 object -> 1  
a = new int[3][2];          // (Step 4) Creates 1 object -> 4  

```
---
## **Total Objects Created:**
- `new int[4][3]` → Creates **1 main object** and **4 sub-arrays** → **Total: 5**
- `new int[4]` → Creates **1 object**
- `new int[2]` → Creates **1 object**
- `new int[3][2]` → Creates **1 main object** and **3 sub-arrays** → **Total: 4**

✅ **Total objects created = 5 + 1 + 1 + 4 = 11**

---

## **Total Objects Eligible for Garbage Collection:**
### **When `a = new int[3][2]` is executed:**
- The reference to the **original `int[4][3]` array** and its **sub-arrays** is lost.
- The **3 newly created sub-arrays** from `new int[3][2]` remain accessible.
- The objects from `new int[4]` and `new int[2]` also become unreachable.

✅ **Total objects eligible for GC = 5 (from `int[4][3]`) + 1 (from `int[4]`) + 1 (from `int[2]`) = 7**

---


### **Example 1:**  

```java
class Test {
    public static void main(String[] args) {
        for (int i = 0; i <= args.length; i++) {
            System.out.println(args[i]);
        }
    }
}
```

# Running the program with three arguments:
java Test A B C

A  
B  
C  
Exception in thread "main" java.lang.ArrayIndexOutOfBoundsException: 3



# Running the program with two arguments:
java Test A B

A  
B  
Exception in thread "main" java.lang.ArrayIndexOutOfBoundsException: 2

# Running the program with no arguments:
java Test 

RE: AI00BE


### **Example 2:**  

```java
class Test {
    public static void main(String[] args) {
        String[] argh = {"X", "Y", "Z"};
        args = argh;
        for (String s : args) {
            System.out.println(s);
        }
    }
}
```

# Running the program with three arguments:
java Test A B C

X  
Y  
Z  



# Running the program with two arguments:
java Test A B

X  
Y   
Z



# Running the program with no arguments:
java Test 

X   
Y   
Z

# **Types of Variables in Java**

Based on the type of values represented by a variable, all variables are divided into two categories:

---

## **Division 1: Based on Value Type**
### **1) Primitive Variables**  
   - Used to represent **primitive values** (e.g., `int`, `char`, `float`, etc.).  
   - **Example:**  
     ```java
     int x = 10;
     ```

### **2) Reference Variables**  
   - Used to refer to **objects**.  
   - **Example:**  
     ```java
     Student s = new Student();
     ```

---

## **Division 2: Based on Declaration & Behavior**  
All variables are classified into **three types**:  

1️⃣ **Instance Variable**  
2️⃣ **Static Variable**  
3️⃣ **Local Variable**  

---

# **Instance Variable in Java**
### **Definition:**  
If the value of a variable varies from **object to object**, it is called an **instance variable**.

### **Key Characteristics:**  
- For **each object**, a **separate copy** of the **instance variable** is created.  
- It **must be declared** within the **class**, but **outside any method, constructor, or block**.  
- It is created at the time of **object creation** and destroyed when the object is **garbage collected**.  
- **Stored in Heap Memory** as a **part of the object**.
- We **cannot access instance variables directly from a static area**, but we **can access them using an object reference**.  
- We **can access instance variables directly from the instance area**.  
- **Instance variables are also known as object-level variables or attributes.**  
- **For instance variables, JVM will always provide default values, so explicit initialization is not required.** 

```java
class Test {
    int x = 10;
    int xx;
    double dd;
    boolean bb;
    String ss;

    public static void main(String[] args) {

        System.out.println(x);   // ❌ CE: non-static variable x cannot be referenced from static context

        Test t = new Test(); // ✅ Creating an object

        System.out.println(t.x); // ✅ Output: 10
        System.out.println(t.xx); // ✅ Output: 0
        System.out.println(t.dd); // ✅ Output: 0.0
        System.out.println(t.bb); // ✅ Output: false
        System.out.println(t.ss); // ✅ Output: null

    }
}
```

### **Example:**  
```java
class Student {
    int rollNo;  // Instance variable
    String name; // Instance variable

    public static void main(String[] args) {
        Student s1 = new Student();
        Student s2 = new Student();

        s1.rollNo = 101;
        s1.name = "Aman";

        s2.rollNo = 102;
        s2.name = "Kumar";

        System.out.println(s1.rollNo + " " + s1.name); // Output: 101 Aman
        System.out.println(s2.rollNo + " " + s2.name); // Output: 102 Kumar
    }
}
```

# **Static Variable in Java**

### **Definition:**  
If the value of a variable **does not vary from object to object**, then it is **not recommended** to declare it as an **instance variable**.  
Instead, such variables should be declared at the **class level** using the `static` modifier.

---

## **Key Characteristics of Static Variables:**
- In the case of **instance variables**, **each object** gets a **separate copy**.  
- In the case of **static variables**, **a single copy** is created **at the class level** and **shared by all objects**.  
- **Static variables should be declared within the class**, but **outside any method, block, or constructor**.  
- **Static variables are created when the class is loaded** and **destroyed when the class is unloaded**.  
- The **scope** of a static variable is the **same as the scope of the `.class` file**.  
- **Stored in the Method Area** (not in Heap memory like instance variables).
- We can access **static variables** either by **object reference** or by **class name**, but it is **recommended to use the class name**.  
- Within the same class, it is **not required to use the class name**; we can access static variables directly.  
- Static variables can be accessed directly from both **instance and static areas**.  
- **For static variables, the JVM provides default values**, so **explicit initialization is not required**.  
- **Static variables are also known as class-level variables or fields**. 

---

## **Java `.class` File Execution Process and `Static variable` creation**
1️⃣ **Start JVM**  
2️⃣ **Create & Start Main Thread**  
3️⃣ **Locate the `Test.class` file**  
4️⃣ **Load `Test.class`** → **Static variables are created**  
5️⃣ **Execute `main()` method**  
6️⃣ **Unload `Test.class`** → **Static variables are destroyed**  
7️⃣ **Terminate Main Thread**  
8️⃣ **Shut down JVM**  

---

## **Example: Static vs Instance Variables**
```java
class Test {
    static int x = 10; // Static variable
    int y = 20;        // Instance variable

    public static void main(String[] args) {

        System.out.println(x);  // Output: 10

        Test t1 = new Test();
        t1.x = 888;  // Modifying static variable using t1
        t1.y = 999;  // Modifying instance variable for t1

        Test t2 = new Test();
        System.out.println(t1.x + "   " + t1.y);  // Output: 888   999
        System.out.println(t2.x + "   " + t2.y);  // Output: 888   20
    }
}
```
## **Note:**  
- `x` is a **static variable**, so **any changes made to it will be reflected across all objects**.  
- `y` is an **instance variable**, meaning **each object has its own separate copy**.  
  - **Modifications to `t1.y` do not affect `t2.y`**, as they belong to different objects.
---

# **Local Variables in Java**  

## **Definition:**  
A **local variable** is a variable that is **declared within a method, constructor, or block** and is only accessible within that scope.  

## **Key Points:**  
- **Local variables are created** when the execution enters the block where they are declared.  
- **They are destroyed** once the block execution completes.  
- **Scope:** Limited to the block in which they are declared.  
- **JVM does not provide default values** for local variables.  
- **Explicit initialization is mandatory** before using a local variable.  
- **Local variables are stored in the stack memory.**  

## **Example:**  

```java
class Test {
    public static void main(String[] args) {
        int x = 10;  // ✅ Local variable (must be initialized before use)
        
        if (x > 5) {
            int y = 20;  // ✅ Local variable inside 'if' block
            System.out.println("x: " + x + ", y: " + y); // Output: x: 10, y: 20
        }

        // System.out.println(y); ❌ Compilation Error (y is out of scope)
    }
}

