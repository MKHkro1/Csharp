程序在[[Csharp语句块]]中

程序语句的固定写法：
完成命令用分号结束
语句中的标点符号用英文

```C#
//引用命名空间(工具包)
using System;
//命名空间(工具包，可自创)
namespace 模板
{  
    //**命名空间代码块**
    //[也是面向对象相关在此处写代码]
    
    //类 （工具）
    class Program
    {   
         //**类代码块** 
         //【面向对象相关在此处写代码】
        
        //函数（工作能做的事情）
        
        //main 主函数：一个程序的主入口
        
         static void Main(string[] args)
        {   
            //**函数的代码块**
            //【基础代码全部都会写在此种代码块中】
            //在控制台中打印出Hello world
            
            //(console是工具包中的一类工具)
            //(console内部也会引用一些源码)
            //WriteLine:做的事情的方法之一
            Console.WriteLine("hello World!");
            
            Console.WriteLine("唐");
        }
    }
    
}

```



```C#
//程序命令；
Console.WriteLine("hello World!");

```

