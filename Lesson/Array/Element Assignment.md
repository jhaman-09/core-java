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
