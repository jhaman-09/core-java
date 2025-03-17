# 🚀 ***Anonymous Arrays*** 🔥  

## 📌 What are Anonymous Arrays?  
Sometimes, we can declare arrays **without a name**. These nameless arrays are called **Anonymous Arrays**.  
The main purpose of an **Anonymous Array** is for **instant use (one-time usage).**  

---

## ⚡ Creating an Anonymous Array:
```java
new int[] {10, 20, 30, 40};     // ✅ Correct
new int[3] = {10, 20, 30, 40};  // ❌ Compile-time Error
```

> ⚠️ **Note:** While creating an anonymous array, we **cannot specify the size**,  
> otherwise, we will get a **compile-time error**.

---

## 🔥 Multi-Dimensional Anonymous Arrays:
```java
new int[][] {{10, 20}, {30, 40, 50}};
```
Yes! We can also create **multi-dimensional anonymous arrays**. 🎯

## 📌 Naming an Anonymous Array  
Based on our requirement, we can **assign a name** to an anonymous array.  
Once named, it is **no longer anonymous**:  

```java
int[] x = new int[]{10, 20, 30};  // ✅ Named array
```

## 🚀 ***Anonymous Arrays in Method Calls*** 🔥  

### 📌 Using Anonymous Arrays in Method Calls  
We can **pass an anonymous array as an argument** to a method.  
This allows us to use **one-time arrays** without explicitly assigning them a name.  

---

### ⚡ Example Code:
```java
class Test {
    public static void main(String[] args) {
        sum(new int[]{10, 20, 30});  // ✅ Passing an anonymous array
    }

    public static void sum(int[] x) {
        int total = 0;
        for (int xx : x) {
            total = total + xx;
        }
        System.out.println("The sum: " + total);  // Output: The sum: 60
    }
}
```

---

### 🔥 Explanation:
- **`new int[]{10, 20, 30}`** → This is an **anonymous array** passed directly to the `sum()` method.
- **`sum(int[] x)`** → The method receives the array and calculates the sum.
- **Enhanced for loop (`for-each`)** → Iterates through each element and adds it to `total`.
- **Final output:** `"The sum: 60"`

---

### 🎯 **Key Takeaways:**
✅ Anonymous arrays **can be passed directly** to methods.  
✅ They are useful when **we don’t need to reuse the array**.  
✅ **Syntax:** `methodName(new dataType[]{values});`  

This approach **saves memory and improves efficiency** for temporary use cases! 🚀🔥  
