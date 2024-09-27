# 学习 C# 笔记
# 目录

# 1. 反射
在C#中，反射（Reflection）是一种强大的机制，它允许程序在运行时获取有关对象类型的信息，并动态地调用方法、访问属性和操作对象。反射能够让你更灵活地处理对象和类型，适用于某些需要动态行为的场景，比如插件系统、序列化、依赖注入等。
    
## 1. 反射的基本概念
反射通常涉及以下几个方面：
  
+ 获取类型信息：使用 Type 类获取对象的类型信息。
+ 创建实例：通过反射可以动态创建对象。
+ 访问成员：可以访问类型的字段、属性、方法等。   
## 2. 使用反射的基本示例
下面是一个简单的示例，演示如何使用反射来获取类信息和访问其成员。
~~~csharp   
using System;   
using System.Reflection;   

public class Person   
{   

    public string Name { get; set; }  
    
    public int Age { get; set; }   

    public void DisplayInfo()      
    {  
        Console.WriteLine($"Name: {Name}, Age: {Age}");   
    }  
}   

class Program   
{
    static void Main()   
    {
        // 创建Person对象
        Person person = new Person();  
        
        // 获取Type对象
        Type type = person.GetType();  
        
        // 获取并设置属性值
        PropertyInfo nameProperty = type.GetProperty("Name");
        nameProperty.SetValue(person, "Alice");   
        
        PropertyInfo ageProperty = type.GetProperty("Age");
        ageProperty.SetValue(person, 30);  
        
        // 调用方法
        MethodInfo displayMethod = type.GetMethod("DisplayInfo");
        displayMethod.Invoke(person, null);   
        
        // 获取所有属性
        PropertyInfo[] properties = type.GetProperties();
        foreach (var prop in properties)
        {
            Console.WriteLine($"属性名: {prop.Name}, 属性值: {prop.GetValue(person)}");
        }
    }
}  
~~~    
## 3. 常用的反射方法  
+ GetType()：获取对象的类型。
+ GetProperties()：获取类型的所有公共属性。
+ GetFields()：获取类型的所有字段。
+ GetMethods()：获取类型的所有方法。
+ Activator.CreateInstance()：动态创建对象实例。
+ Invoke()：动态调用方法。
### 4. 反射的注意事项   
+ 性能：反射相对较慢，因为它在运行时进行类型查找和方法调用，因此不应在性能敏感的场合频繁使用。
+ 安全性：在某些情况下，反射可能会暴露不应被访问的内部实现，因此需谨慎使用。
### 5. 应用场景
+ 插件架构：可通过反射动态加载和使用插件。
+ 序列化与反序列化：通过反射获取对象的属性进行数据转换。
+ 依赖注入框架：通过反射实现自动构造和注入依赖项。    
总之，反射提供了一种在运行时处理类型和对象的方式，能够增强程序的灵活性和动态性，但在使用时要注意性能和安全性。
