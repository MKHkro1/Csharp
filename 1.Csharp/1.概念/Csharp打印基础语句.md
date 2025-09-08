# 知识点
输出：
WriteLine
Write
输入：
ReadLine
ReadKey

# 讲解
```C#
//引用命名空间
using System;
//命名空间
namespace 模板
{  
    //类
    class Program
    {    //函数
         static void Main(string[] args)
        {   //在控制台中打印出Hello world
            
            //在控制台 打印出一行信息 打印信息结束后会自动空一行            
            Console.WriteLine("hello World!");
            
            //如果是双引号中的内容，对于符号没有特别要求
            //其他需要英文符号
            
            //在控制台 打印出一行信息 打印信息结束后会自动空一行 
            Console.Write("hello World!");
            
              //检测玩家输入的代码（回车后才会继续执行）
              //玩家可以输入很多信息
            Console.WriteLine("请玩家输入");
            Console.ReadLine();
            Console.WriteLine("玩家输入完毕");
            
            //检测玩家是否按键（任意键可继续执行）
            Console.WriteLine("请玩家输入");
            Console.ReadKey();
            Console.WriteLine("玩家输入完毕");
            
            
        }
    }
    
}

```

# 实操
Test
1. Console. Write and Console. WriteLine
2. Console. ReadKey and Console. ReadLine
3. Ask player for some information
4. Talk with player 
5. Output a 10`*`10 hollow star square matrix

```C#
//引用命名空间
using System;
//命名空间
namespace 模板
{  
    //类
    class Program
    {    //函数
         static void Main(string[] args)
        {   //在控制台中打印出Hello world
            Console.WriteLine("你喜欢什么运动");
            Console.ReadLine();
            Console.WriteLine("哈哈，好巧，我也喜欢这个运动");
            
            //输出一个10*10的空心星型方阵
            Console.WriteLine("**********");
            Console.WriteLine("*        *");
            Console.WriteLine("*        *");
            Console.WriteLine("*        *");
            Console.WriteLine("*        *");
            Console.WriteLine("*        *");
            Console.WriteLine("*        *");
            Console.WriteLine("*        *");
            Console.WriteLine("**********");
        }
    }
    
}

```