Polymorphsisim

Method Overloading

Doesn't is always occur in the same class 

❓ Q2: Overloading vs Overriding confusion
class A {
    void test(int a) {}
}

class B extends A {
    void test(long a) {}
}

👉 ✅ This is NOT overriding — it’s overloading

💡 Signature is different (int vs long)


If a class is related with IS-A Realtionship
How this is Overloading is applicable ?


----

How to Call parent Method and Child Method 
In Polymorphsisim ?



---


❓ Q3: Polymorphism trap (reference vs object)
class A {
    void test(int a) { System.out.println("A-int"); }
}

class B extends A {
    void test(long a) { System.out.println("B-long"); }
}

A obj = new B();
obj.test(10);

👉 Output: A-int

💡 Why?

Overloading is resolved at compile-time
Compiler checks reference type (A) → only sees test(int)
Runtime polymorphism does NOT apply here


