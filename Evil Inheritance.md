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
     public abstract void speak();
}

public class Vietnamese : Person
{
    @Override
    public void speak() {
        System.out.println("speak vietnamese");
    }
}

public class Dutch : Person
{
     @Override
    public void speak() {
        System.out.println("speak Dutch");
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

Nguyên tắc này có thể hiểu là ko nên sử dụng inheritance khi 2 class ko thực sự
có quan hệ IS-A:

```cs
class Person {
    public int PersonId { get; set; }
    public string Name { get; set; }
    public DateTime DateOfBirth { get; set; }
    public string Address { get; set; }
}

class Customer : Person {
    public int CustomerId { get; set; }
    public DateTime JoinedDate { get; set; }
}

class Staff : Person {
    public int StaffId { get; set; }
    public string JobTitle { get; set; }
}

static void SendEmailToCustomers(IEnumerable<Person> everyone) {
    foreach(Person p in everyone)
        if(p is Customer)
            SendEmail(p);
}
```

Hàm SendEmailToCustomers() trên sẽ bị sai khi có 1 Person vừa là Customer vừa là Staff (
Người này sẽ bị gửi email 2 lần). Nguyên nhân là do Custommer và Staff ko có quan hệ IS-A với
class Person. Chúng chỉ là role, và có thể thay đổi theo thời gian.

```cs
class Person {
    public int PersonId { get; set; }
    public string Name { get; set; }
    public DateTime DateOfBirth { get; set; }
    public string Address { get; set; }
    public List<Role> Roles {get; set;}
}

class Role{
    public int Id { get; set; }
    public void display(){}
}

class Staff : Role {
    public string JobTitle { get; set; }
}

class Custommer: Role{
    public DateTime JoinedDate { get; set; }
}
```

