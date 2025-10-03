# Unity 打包形式
Mono

IL 2CPP：防反编译，看不到具体代码

Unityplayer 显示版本号

UnityCrashHandler 32/64 显示位数

# 框架下载
选择下载（mono/IL 2CPP）
存在 GameAssembly. Dll

下载对应版本号之后移入


# 首次加载
如果是 steam 游戏，不要使用快捷方式启动
接入了 steam  API ，强制从 steam 重启了一遍，可能会导致 mod 的接入失效

首次加载游戏之后，将在 BeplnEx多出几个文件夹，即代表框架安装成功

注意需要区别下载mono 和IL 2 的 BeplnEx 框架

根据 BeplnEx 协议，首次启动要求从github 库中下载对应的必要文件
严格来讲，这些文件不能在传播unity-libs

