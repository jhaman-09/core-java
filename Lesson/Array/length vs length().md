# 🚀 ***Length vs Length()*** 🔥
## 📌 **Length in Arrays**

```java
int[] x = new int[6];

System.out.println(x.length()); ❌❌ // CE: cannot find symbol method length()
                                      // location: class int[]

System.out.println(x.length); ✅✅ // 🎯 Correct usage
```


✅ Key Points:
- Length is a final variable applicable for arrays.
- The length variable represents the size of the array.

## 📌 **Length() Method**

```java
String s = "Aman";
System.out.println(s.length) ❌❌ // CE: cannot find symbol 
                                   // symbol: variable length
                                   // location: class java.lang.String 

System.out.println(s.length())  ✅✅ // 🎯 correct usage
```
✅ Key Points:
- Length method is final method applicable for String objects.
- Length method returns number of charactors present in the String.

## 📝 **Note**  

- 🔹 `length` variable is **applicable for arrays** but ❌ **not for String objects**.  
- 🔹 `length()` **method is applicable for String objects** but ❌ **not for arrays**.  
