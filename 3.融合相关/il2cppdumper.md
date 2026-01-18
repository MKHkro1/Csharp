普通PC端IL2Cpp Unity游戏逆向方法体代码记录
# **1.准备**

IDA（这里使用IDA 9.0 Pro）
IL2CppDumper（下载链接：https://github.com/Perfare/Il2CppDumper）
一个用IL2Cpp打包的Unity游戏（这里以植物大战僵尸融合版2.4.2举例）
一个好用一点的AI~~（如果你能看懂IDA反编译出来的C代码就不需要了）~~

# **2.反编译符号信息**

解压下载下来的IL2CppDumper
![image.png](https://picgo18719498306.oss-cn-guangzhou.aliyuncs.com/20251004161830409.png)
`解压好的IL2CppDumperr（6.7.46）`

在IL2CppDumper目录下新建input和output文件夹

往input目录下放入游戏的GameAssembly.dll和global-metadata.dat，并在input目录里创建一个il2cpp_decompilation.bat文件，输入以下内容

```
..\Il2CppDumper.exe GameAssembly.dll global-metadata.dat ..\output
```
![image.png](https://picgo18719498306.oss-cn-guangzhou.aliyuncs.com/20251004162024159.png)
`完成好的input目录`

双击运行il2cpp_decompilation.bat
命令行显示

```
Done!

Press any key to exit...
```

就说明反编译成功了，随便按个键退出就可以了
然后打开刚刚创建的output目录检查一下有东西就可以了

# **2.IDA反编译**

打开你下载的IDA
将游戏的GameAssembly.dll拖进去
然后会显示一个加载pdb的页面~~（虽然一般你也查不到）~~，这个不用管，后面会通过脚本加载
![image.png](https://picgo18719498306.oss-cn-guangzhou.aliyuncs.com/20251004162500962.png)

![image.png](https://picgo18719498306.oss-cn-guangzhou.aliyuncs.com/20251004162530537.png)

点击左上角File -> Script File...
在打开的文件选择页面中选择解压下来的IL2CppDumper根目录下的ida_with_struct_py3.py（有的说用ida_py3.py），双击选择
然后会有选择.json和.h文件的窗口，分别选择 IL2CppDumper根目录\output\script.json 和 IL2CppDumper根目录\output\il2cpp.h，选择完成之后慢慢等就是了

这期间可能会出现各种Warning窗口，一路OK点过去就可以了

![image.png](https://picgo18719498306.oss-cn-guangzhou.aliyuncs.com/20251004162704318.png)

![image.png](https://picgo18719498306.oss-cn-guangzhou.aliyuncs.com/20251004162746557.png)
![image.png](https://picgo18719498306.oss-cn-guangzhou.aliyuncs.com/20251222010205376.png)

![image.png](https://picgo18719498306.oss-cn-guangzhou.aliyuncs.com/20251004162816960.png)

![image.png](https://picgo18719498306.oss-cn-guangzhou.aliyuncs.com/20251004162848628.png)

完成之后在左边的导航栏双击你要看的方法就会跳转到它的汇编定义，然后按F5就可以看到这个反编译后的伪代码了

# **3.AI神力****~~（如果你能看懂伪代码就可以直接跳过了）~~

打开一个好用的AI，把转换后的伪代码粘贴给它，让它转换成你看得懂的代码就完成了


# 4. 注意
要下 python 环境的 IDA

反汇编之后按F5之后是转换为伪代码(Pseudocode)，不是C

### **重新分析整个程序**

`菜单操作：Analysis → Reanalyze program 快捷键：Ctrl + F5

# 导出文件
![image.png](https://picgo18719498306.oss-cn-guangzhou.aliyuncs.com/20260118122628765.png)

`