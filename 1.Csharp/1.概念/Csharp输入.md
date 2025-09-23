依据语言规则进行从上到下的书写

  自己写的
    ↑                           （调用）
    ↓
系统内置代码

代码块的相互调用 ：API 应用程序接口
用来提供应用程序与开发人员基于某软件或硬件得以访问的一组例程，而又无需访问源码，或理解内部的工作机制的细节（拼好码），从而实现许多功能（相互不停地调用）
```C#
//引用命名空间
using System;
//命名空间
namespace 模板{  
    //类
    class Program
    {    //函数
         static void Main(string[] args)
        {   //在控制台中打印出Hello world
            Console.WriteLine("hello World!");
        }
    }
    
}

```
系统内置定义

Main 方法

