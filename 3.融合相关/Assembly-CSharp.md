# **Unity IL2Cpp打包（通用方法）**

若游戏使用**IL2Cpp**（而非Mono）打包，原`Assembly-CSharp.dll`会被转换为`libil2cpp.so`（原生库）和`global-metadata.dat`（元数据），需通过**Il2CppDumper**还原DLL：

- **步骤1：下载Il2CppDumper**​
    
    从GitHub开源仓库（https://github.com/Perfare/Il2CppDumper/releases）下载最新版本，解压得到`Il2CppDumper.exe`。
    
- **步骤2：获取游戏文件**​
    
    - Android：从APK中提取`libil2cpp.so`（位于`lib/armeabi-v7a`或`arm64-v8a`文件夹）和`global-metadata.dat`（位于`assets/bin/Data`）。
        
    - iOS：从IPA中提取`libil2cpp.dylib`（位于`Payload/应用名.app`）和`global-metadata.dat`（位于`Data/Managed`）。
        
    
- **步骤3：运行Il2CppDumper**​
    
    将`libil2cpp.so`（或`libil2cpp.dylib`）和`global-metadata.dat`复制到Il2CppDumper的`Input`文件夹，在`Input`文件夹中创建`run.bat`（Windows）或`run.sh`（macOS），内容如下：
    
    `Il2CppDumper.exe ..\Input\libil2cpp.so ..\Input\global-metadata.dat ..\Output`
    
    运行批处理文件，即可在`Output/DummyDll`文件夹中找到`Assembly-CSharp.dll`（伪DLL，包含反编译后的类型和方法信息）。