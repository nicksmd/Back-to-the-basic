##### Các trường hợp ko sử dụng inheritance:

1. Khi việc dùng inheritance chỉ tạo ra các class rỗng và vô nghĩa

```cs
public class Person
{
     public int Id { get; set; }
     public string Name { get; set; }
}

public class Player : Person
{
}
```

Class Person trong đoạn code trên là vô dụng

2. Khi chỉ kế thừa attributes (field)

```cs
public class Person
{
     public int Id { get; set; }
     public string Name { get; set; }
}

public class Player : Person
{
     public byte Number { get; set; }
}

public class Coach : Person
{
     public byte YearsOfExperience { get; set;
}
```

Nên sử dụng khi có sự kế thừa behavior (method):
```cs
public class Person
{
     public void eat() {  }
     public void sleep() {  }
     public abstract void talk();
}

public class Vietnamese : Person
{
    @Override
    public void talk() {
        System.out.println("talk vietnamese");
    }
}

public class Dutch : Person
{
     @Override
    public void talk() {
        System.out.println("talk Dutch");
    }
}
```

3. Khi vi phạm LISKOV SUBSTITUTION PRINCIPLE [LSP]

> if S is a subtype of T, then objects of type T may be replaced with objects of type S.

```java
public class Bird{
    public void fly(){}
}
public class Duck extends Bird{}
public class Ostrich extends Bird{}
```

Ostrich cũng là chim nhưng ko thể bay. Trong trường hợp này, behavior Bay không
giống nhau ở mọi loài chim => nên tách thành 1 interface sử dụng Composition:

```java
public class Bird{
}
public class FlyingBirds extends Bird{
    public void fly(){}
}
public class Duck extends FlyingBirds{}
public class Ostrich extends Bird{}
```
