![4298e52c01accd6623ad8b04d139df72.png](https://picgo18719498306.oss-cn-guangzhou.aliyuncs.com/4298e52c01accd6623ad8b04d139df72.png)

怎么把 System. Type 转成 Il 2 CppSystem. Type 啊

直接 using il 2 cpp 的就行啊
要是两个都要用到还不能替换的话
有个 using il 2 cppsystem. Type type 的用法

窝是说一个 System. Type 的变量怎么把它转成 Il 2 CppSystem. Type 的变量

不能强转吗

不可以捏
![a0037f9f64d112f9f60bb4bf1451c22e.png](https://picgo18719498306.oss-cn-guangzhou.aliyuncs.com/a0037f9f64d112f9f60bb4bf1451c22e.png)

用的 typeof 是吧

对

看看这一行

我记得我之前写的时候也遇到了这个情况

窝好像找到了

Il2CppType.From（？）

有个 gettype

Il 2 CppSystem.Type.GetType (name);

Name 传的是字符串

