# IDA Pro 9.2.250908

## 前言


1. 添加IDA Pro 9.2.250908安装配置教程
    
2. 优化IDAPython安装部分
    
    使用便携版python而非安装版
    
3. 精简插件安装部分
    
    分为核心插件和其他插件,核心插件推荐安装,其他插件根据个人需求安装
    
4. 总结IDA的优化设置
    
    可修改ida.cfg和注册表进行优化, 已集成到打包的IDA和初始化工具中
    
5. 优化初始化IDA工具
    
    执行3个操作: 指定IDAPython路径, 禁用IDA自动更新和IDA9新式快捷键, 创建桌面快捷方式
    

提供打包好的IDA Pro 9.2.7z :

文件链接: https://pan.baidu.com/s/13cPJRT-1a0NgEPByMSIl5A?pwd=244c

1. 解压后运行InitIDA.exe一键初始化即可使用
    
2. 默认使用内嵌的便携版python3.11.9作为idapython
    
3. 修改了ida.cfg的部分配置进行优化
    
4. 默认安装了核心插件及其python依赖
    
    Keypatch, patching, DataExportPlus, findcrypt-yara, hrtng, LazyIDA, auto-enum, bindiff
    

注意:

1. **IDA所在路径不能有中文**, 否则会导致bug
2. IDAPython运行pip时需要进入IDAPython所在文件夹, 并通过 "python -m pip" 形式的命令调用
3. 打包版可能出现如下报错无法打开ida (手动安装不会有该问题)  
    由于qt引发该bug,具体细节暂时未知,经测试删除plugins中的notepad-md.py, patching.py, LazyIDA.py 以及 patching目录后可以正常启动ida  
    ![](https://bbs.kanxue.com/upload/attach/202509/871975_CYRJYWYNUCMJFA5.webp)  
    ![](https://bbs.kanxue.com/upload/attach/202509/871975_5ACC79UJFZ4TEYP.webp)

提供以下文件供师傅们自行安装配置:

文件链接: https://pan.baidu.com/s/1Rf1LU1tp985Ic4_IiN-Zpg?pwd=edvk

1. 各平台的IDA Pro 9.2安装程序(带keygen)
2. IDA Pro 9.2 SDK
3. 个人整理的IDA插件合集,包括核心插件和其他插件
4. 内嵌版python 3.11.9

**声明: 文章资源仅作学习交流使用，不得用于商业或者非法用途，请测试后尽快删除，购买正版进行支持**

## 更新部分

详情请参考https://docs.hex-rays.com/release-notes/9_2

主要更新如下:

1. Decompiler增强对Golang的支持
    
    IDA 9.1分析golang程序,函数参数较为丑陋
    
    ![](https://bbs.kanxue.com/upload/attach/202509/968342_DYJPH93ZHZPAVJP.png)
    
    IDA 9.2分析golang程序,结构清晰明显
    
    ![](https://bbs.kanxue.com/upload/attach/202509/968342_ATPHCX92KFE6AG3.png)
    
2. UI升级
    
    主要从QT5升级到QT6,受此影响可能导致部分插件不兼容,所以IDA官方提供了QT5兼容层PyQt5 Shims
    
3. Decompiler升级
    
    新增Microcode Viewer使用Ctrl-Shift-F8打开,可观察到Decompiler在反汇编和伪代码生成过程中产生的微码
    
4. 扩展各CPU架构的反汇编指令集
    
5. Debugger升级,调试时寄存器窗口信息更加详细美观
    
    ![](https://bbs.kanxue.com/upload/attach/202509/968342_RUD44G576BG8BRB.png)
    
6. 开源IDA SDK https://github.com/HexRaysSA/ida-sdk
    

## 安装破解

运行安装程序后,将keygen脚本拖动到ida目录内,使用--oneshot选项执行一键patch后即可使用

![43-ida92-keygen](https://bbs.kanxue.com/upload/attach/202509/968342_8WWMEWD4FP9H759.png)

## 优化设置

### cfg/ida.cfg

cfg文件中主要修改以下设置

|   |   |
|---|---|
|1<br><br>2<br><br>3<br><br>4<br><br>5<br><br>6<br><br>7<br><br>8|`STORE_USER_INFO` `=` `YES` `-``> NO`          `/``/` `关闭idb存储用户信息`<br><br>`OPCODE_BYTES` `=` `0` `-``>` `10`                   `/``/` `反汇编界面显示``10``字节指令硬编码`<br><br>`INDENTION` `=` `16` `-``>` `0`                  `/``/` `硬编码和汇编指令的间距设置为``0`<br><br>`SHOW_BASIC_BLOCKS` `=` `NO` `-``> YES`            `/``/` `在基本块的末尾生成一个空行`<br><br>`SHOW_XREFS` `=` `2` `-``>` `16`                     `/``/` `增加交叉引用显示数`<br><br>`SHOW_SOURCE_LINNUM`  `=` `NO` `-``> YES`      `/``/` `显示源码行号`<br><br>`SHOW_SP` `=` `NO` `-``> YES`                  `/``/` `显示SP指针偏移`<br><br>`ENCODING_CULTURES 添加 GB2312: Chinese`  `/``/` `开启中文字符串显示`|

### 注册表键

IDA的注册表键主要修改以下项目,包括指定IDAPython路径, 禁用自动更新, 禁用新版快捷键

|   |   |
|---|---|
|1<br><br>2<br><br>3<br><br>4<br><br>5<br><br>6<br><br>7|`# 以下注册表键均位于HKEY_USERS\HKEY_CURRENT_USER\SOFTWARE\Hex-Rays\IDA下`<br><br>`# Python3TargetDLL          IDAPython路径`<br><br>`# AutoCheckUpdates -> 0      关闭自动检查更新`<br><br>`# AutoRequestUpdates -> 0    关闭自动请求更新`<br><br>`# AutoUseLumina -> 0     关闭自动使用Lumina`<br><br>`# Use90ShortcutSet -> 0      关闭IDA9的新快捷键,默认使用经典快捷键`|

## 初始化工具

使用pyinstaller打包以下初始化脚本为InitIDA.exe, 在IDA.exe所在目录中运行即可

|   |   |
|---|---|
|1<br><br>2<br><br>3<br><br>4<br><br>5<br><br>6<br><br>7<br><br>8<br><br>9<br><br>10<br><br>11<br><br>12<br><br>13<br><br>14<br><br>15<br><br>16<br><br>17<br><br>18<br><br>19<br><br>20<br><br>21<br><br>22<br><br>23<br><br>24<br><br>25<br><br>26<br><br>27<br><br>28<br><br>29<br><br>30<br><br>31<br><br>32<br><br>33<br><br>34<br><br>35<br><br>36<br><br>37<br><br>38<br><br>39<br><br>40<br><br>41<br><br>42<br><br>43<br><br>44<br><br>45<br><br>46<br><br>47<br><br>48<br><br>49<br><br>50<br><br>51<br><br>52<br><br>53<br><br>54<br><br>55<br><br>56<br><br>57<br><br>58<br><br>59<br><br>60<br><br>61<br><br>62<br><br>63<br><br>64<br><br>65<br><br>66<br><br>67<br><br>68<br><br>69<br><br>70<br><br>71<br><br>72<br><br>73<br><br>74<br><br>75<br><br>76<br><br>77<br><br>78<br><br>79<br><br>80<br><br>81<br><br>82<br><br>83<br><br>84<br><br>85<br><br>86<br><br>87<br><br>88<br><br>89<br><br>90<br><br>91<br><br>92<br><br>93<br><br>94<br><br>95<br><br>96<br><br>97<br><br>98<br><br>99<br><br>100<br><br>101<br><br>102<br><br>103<br><br>104<br><br>105<br><br>106<br><br>107<br><br>108<br><br>109<br><br>110<br><br>111<br><br>112<br><br>113<br><br>114<br><br>115<br><br>116<br><br>117<br><br>118<br><br>119<br><br>120<br><br>121<br><br>122<br><br>123<br><br>124<br><br>125<br><br>126<br><br>127|`import` `os`<br><br>`import` `winreg`<br><br>`import` `win32com.client`<br><br>`key_path` `=` `r``"SOFTWARE\Hex-Rays\IDA"`<br><br>`cwd` `=` `os.getcwd()`<br><br>`choice_yes_items``=``('``','``y``','``Y``','``yes')`<br><br>`# 配置IDAPython路径`<br><br>`def` `set_idapy_path(idapy_path):`<br><br>    `try``:`<br><br>        `key` `=` `winreg.CreateKey(winreg.HKEY_CURRENT_USER, key_path)`<br><br>        `with key:`<br><br>            `# 存在python3.dll`<br><br>            `idapy_dll_path``=``os.path.join(idapy_path,``"python3.dll"``)`<br><br>            `print``(f``"Setting IDAPython path to: {idapy_dll_path}"``)`<br><br>            `if` `idapy_dll_path` `and` `os.path.isfile(idapy_dll_path):`<br><br>                `winreg.SetValueEx(key,` `"Python3TargetDLL"``,` `0``, winreg.REG_SZ, idapy_dll_path)`<br><br>                `print``(``"Setted IDAPython path successfully."``)`<br><br>        `return` `True`<br><br>    `except` `Exception as e:`<br><br>        `print``(f``"Failed to set IDAPython path: {e}"``)`<br><br>        `return` `False`<br><br>`# 禁用IDA自动更新`<br><br>`def` `ban_ida_auto_update(disable):`<br><br>    `try``:`<br><br>        `key` `=` `winreg.CreateKey(winreg.HKEY_CURRENT_USER, key_path)`<br><br>        `with key:`<br><br>            `if` `disable:`<br><br>                `winreg.SetValueEx(key,` `"AutoCheckUpdates"``,` `0``, winreg.REG_DWORD,` `0``)`<br><br>                `winreg.SetValueEx(key,` `"AutoRequestUpdates"``,` `0``, winreg.REG_DWORD,` `0``)`<br><br>                `winreg.SetValueEx(key,` `"AutoUseLumina"``,` `0``, winreg.REG_DWORD,` `0``)`<br><br>        `print``(``"Disabled IDA auto update successfully."``)`<br><br>        `return` `True`<br><br>    `except` `Exception as e:`<br><br>        `print``(f``"Failed to disable IDA auto update: {e}"``)`<br><br>        `return` `False`<br><br>`# 禁用IDA9快捷键`<br><br>`def` `ban_ida90_shortcut(unable):`<br><br>    `try``:`<br><br>        `key` `=` `winreg.CreateKey(winreg.HKEY_CURRENT_USER, key_path)`<br><br>        `with key:`<br><br>            `if` `unable:`<br><br>                `winreg.SetValueEx(key,` `"Use90ShortcutSet"``,` `0``, winreg.REG_DWORD,` `0``)`<br><br>                `print``(``"Disabled IDA90 Shortcut Style successfully."``)`<br><br>        `return` `True`<br><br>    `except` `Exception as e:`<br><br>        `print``(f``"Failed to set IDA shortcut style: {e}"``)`<br><br>        `return` `False`<br><br>`# 配置IDA注册表`<br><br>`def` `set_ida_regs(default):`<br><br>    `if` `default:`<br><br>        `print``(``"\nSetting IDA Registries..."``)`<br><br>        `set_idapy_path(os.path.join(cwd, r``"python311"``))` `# 默认使用内嵌的python3.11.9`<br><br>        `ban_ida_auto_update(``True``)`<br><br>        `ban_ida90_shortcut(``True``)`<br><br>    `else``:`<br><br>        `idapy_path``=``input``(``"\nInput your IDAPython path: "``)`<br><br>        `set_idapy_path(idapy_path)`<br><br>        `au_choice``=``input``(``"\nDisable IDA auto update?(Y/N y/n): "``).lower()`<br><br>        `if` `au_choice` `in` `choice_yes_items:`<br><br>            `ban_ida_auto_update(``True``)`<br><br>        `sc_choice``=``input``(``"\nUse old-style shortcut?(Y/N y/n): "``).lower()`<br><br>        `if` `sc_choice` `in` `choice_yes_items:`<br><br>            `ban_ida90_shortcut(``True``)`<br><br>    `print``(``"All IDA registry settings are done."``)`<br><br>`# 创建桌面快捷方式`<br><br>`def` `create_shortcut(target):`<br><br>    `name``=``"IDA Pro 9.2"`<br><br>    `try``:`<br><br>        `# 通过注册表获取Desktop路径`<br><br>        `key` `=` `winreg.OpenKey(winreg.HKEY_CURRENT_USER,r``"Software\Microsoft\Windows\CurrentVersion\Explorer\User Shell Folders"``)`<br><br>        `desktop_path, _` `=` `winreg.QueryValueEx(key,` `"Desktop"``)`<br><br>        `winreg.CloseKey(key)`<br><br>        `desktop``=``os.path.expandvars(desktop_path)` `# 展开可能的环境变量`<br><br>        `#desktop = os.path.join(os.path.expanduser("~"), "Desktop") # 获取当前用户的主目录路径`<br><br>        `shortcut_path` `=` `os.path.join(desktop, f``"{name}.lnk"``)`<br><br>        `shell` `=` `win32com.client.Dispatch(``"WScript.Shell"``)`<br><br>        `shortcut` `=` `shell.CreateShortcut(shortcut_path)`<br><br>        `shortcut.TargetPath` `=` `target`<br><br>        `shortcut.WorkingDirectory` `=` `os.path.dirname(target)`<br><br>        `shortcut.Description` `=` `"The Interactive Disassembler"`<br><br>        `shortcut.Save()`<br><br>        `print``(``"Created shortcut on Desktop successfully."``)`<br><br>    `except` `Exception as e:`<br><br>        `print``(``"Failed to create a shortcut."``, e)`<br><br>    `return` `True`<br><br>`def` `main():`<br><br>    `print``(``"========================================================================"``)`<br><br>    `print``(``"         IDA Initilizer created by OrientalGlass (2025-09-13)           "``)`<br><br>    `print``(``"========================================================================"``)`<br><br>    `# 构建路径配置`<br><br>    `ida_path` `=` `os.path.join(cwd,` `"ida.exe"``)`          `# IDA主程序`<br><br>    `# 检测IDA路径`<br><br>    `if` `os.path.exists(ida_path)` `=``=``False``:`<br><br>        `print``(``"Error: please run this initilizer in IDA directory"``)`<br><br>        `return`<br><br>    `else``:`<br><br>        `print``(f``"IDA Path: {ida_path}"``)`<br><br>    `# 主配置流程`<br><br>    `print``(``"\n------------------------------------------------------------"``)`<br><br>    `choice` `=` `input``(``"\nUse default initialization settings?(Y/N y/n): "``).lower()`<br><br>    `if` `choice` `in` `choice_yes_items:`<br><br>        `set_ida_regs(``True``)`<br><br>        `create_shortcut(ida_path)`<br><br>    `else``:`<br><br>        `# 手动配置模式`<br><br>        `set_ida_regs(``False``)`<br><br>        `sc_choice` `=` `input``(``"\nCreate desktop shortcut?(Y/N y/n): "``).lower()`<br><br>        `if` `sc_choice` `in` `choice_yes_items:`<br><br>            `create_shortcut(ida_path)`<br><br>`if` `__name__` `=``=` `"__main__"``:`<br><br>    `main()`|

## IDAPython

使用python便携版(内嵌版)方便管理和迁移IDAPython环境,并且不修改系统配置

但安装时需要注意直接解压的便携版不包括pip,需要额外安装配置

1. 下载并解压便携版
    
    https://www.python.org/downloads/windows
    
    ![](https://bbs.kanxue.com/upload/attach/202509/968342_RU3QFBYTQXE3UJ3.png)
    
2. 下载并执行get-pip脚本
    
    https://bootstrap.pypa.io/get-pip.py
    
    下载后拖动到第1步解压的便携版python文件夹中,并启动cmd运行脚本
    
    |   |   |
    |---|---|
    |1|`python get``-``pip.py`|
    
    ![](https://bbs.kanxue.com/upload/attach/202509/968342_W36BVSXSMD87KDM.png)
    
    安装后会多出Lib和Scripts文件夹,pip.exe便在Scripts中,但此时无法直接使用pip
    
3. 设置pth文件
    
    打开python311._pth文件,将"import site"的注释取消
    
    ![](https://bbs.kanxue.com/upload/attach/202509/968342_ZZ3QW3R4W5J8VV5.png)
    
    之后使用命令验证是否安装成功
    
    |   |   |
    |---|---|
    |1|`python` `-``m pip` `-``-``version`|
    
    如果安装成功则输出如下
    
    ![](https://bbs.kanxue.com/upload/attach/202509/968342_VBJWDN46PB8JR7Q.png)
    
    如果没有设置._pth文件则会报错"No module named pip",参考https://stackoverflow.com/questions/32639074/why-am-i-getting-importerror-no-module-named-pip-right-after-installing-pip
    
4. 设置idapython路径
    
    |   |   |
    |---|---|
    |1|`idapyswitch.exe` `-``-``force``-``path .\python311\python3.dll`|
    

## 插件安装

### PyQt5 Shims

ida虽然从QT5升级为QT6,但为了插件的兼容性,提供了**PyQt5 Shims兼容层**

详细参考https://docs.hex-rays.com/user-guide/plugins/migrating-pyqt5-code-to-pyside6

开启该支持有2种方式:

1. 等待ida检测到不兼容QT6的插件
    
    检测到不兼容的插件时,会弹窗如下,选择Yes即可
    
    ![](https://bbs.kanxue.com/upload/attach/202509/968342_3YRP9NKHEU94JJ2.png)
    
2. 手动设置
    
    在ida/cfg/idapython.cfg文件中,修改最后一行的IDAPYTHON_USE_PYQT5_SHIM赋值为1即可
    
    ![](https://bbs.kanxue.com/upload/attach/202509/968342_UQBF2MM4MJ88KXN.png)
    

### 核心插件

个人使用一段时间ida9.1后,总结出较为核心的几个插件,其余插件根据个人需要选择性安装即可

|插件名|作用|安装方法|备注|
|---|---|---|---|
|[Keypatch](https://bbs.kanxue.com/elink@7e4K9s2c8@1M7s2y4Q4x3@1q4Q4x3V1k6Q4x3V1k6Y4K9i4c8Z5N6h3u0Q4x3X3g2U0L8$3#2Q4x3V1k6C8k6i4W2K6N6r3!0F1k6g2\)9J5k6r3g2F1k6$3W2F1k6g2\)9J5c8X3E0W2P5i4m8S2N6r3y4Z5)|patch汇编指令|将Keypatch.py复制到plugins目录|支持9.2  <br>使用前需要安装keystone-engine和six模块  <br>"python -m pip install keystone-engine"  <br>注意: 是keystone-engine不是keystone  <br>"python -m pip install six"  <br>适配IDA9的keypatch: https://bbs.kanxue.com/thread-282852.htm|
|[Patching](https://bbs.kanxue.com/elink@d84K9s2c8@1M7s2y4Q4x3@1q4Q4x3V1k6Q4x3V1k6Y4K9i4c8Z5N6h3u0Q4x3X3g2U0L8$3#2Q4x3V1k6Y4j5h3q4K6k6h3c8W2L8r3g2F1i4K6u0r3M7r3q4@1j5$3S2A6L8X3M7%60.)|快速patch16进制|将Patching文件夹和Patching.py复制到plugins目录|不直接支持9.2,需开启PyQt5 Shims兼容使用|
|[DataExportPlus](https://bbs.kanxue.com/elink@e8eK9s2c8@1M7s2y4Q4x3@1q4Q4x3V1k6Q4x3V1k6Y4K9i4c8Z5N6h3u0Q4x3X3g2U0L8$3#2Q4x3V1k6w2M7X3W2W2N6s2Z5%4i4K6u0r3d9f1c8m8i4K6u0V1c8r3q4@1j5f1g2^5M7r3!0J5N6q4m8D9N6i4x3%60.)|shift+e数据提取强化版|将DataExportPlus.py复制到plugins目录|支持9.2|
|[findcrypt-yara](https://bbs.kanxue.com/elink@c13K9s2c8@1M7s2y4Q4x3@1q4Q4x3V1k6Q4x3V1k6Y4K9i4c8Z5N6h3u0Q4x3X3g2U0L8$3#2Q4x3V1k6H3L8$3I4&6L8h3!0J5k6W2\)9J5c8X3k6A6L8X3c8U0M7Y4W2H3N6q4\)9J5k6s2W2S2M7X3p5%60.)|搜索常见加密算法特征常数|将findcrypt3.py和findcrypt3.rules复制到ida/plugins目录|支持9.2  <br>使用前需要idapython安装yara-pyhon(注意不是yara) "python -m pip install yara-python "  <br>注意: 该插件在python3.8环境下无法运行|
|[hrtng](https://bbs.kanxue.com/elink@1a7K9s2c8@1M7s2y4Q4x3@1q4Q4x3V1k6Q4x3V1k6Y4K9i4c8Z5N6h3u0Q4x3X3g2U0L8$3#2Q4x3V1k6w2j5i4y4H3k6i4u0K6K9%4W2x3j5h3u0Q4x3V1k6Z5M7Y4c8F1k6H3%60.%60.)|去除OLLVM混淆,栈字符串识别,高亮括号,解密字符串等|plugins/windows/对应版本号/hrtng.dll到plugins目录|支持9.2  <br>另外提供以下文件,拖动到ida/plugins下生效:  <br>ida的md编辑器插件[notepad-md.py](https://bbs.kanxue.com/elink@f45K9s2c8@1M7s2y4Q4x3@1q4Q4x3V1k6Q4x3V1k6Y4K9i4c8Z5N6h3u0Q4x3X3g2U0L8$3#2Q4x3V1k6w2j5i4y4H3k6i4u0K6K9%4W2x3j5h3u0Q4x3V1k6Z5M7Y4c8F1k6#2\)9J5c8X3u0D9L8$3u0Q4x3V1k6E0j5i4y4@1k6i4u0Q4x3V1k6T1K9h3&6Q4x3V1k6H3L8s2g2Y4K9h3&6K6i4K6u0r3L8X3!0@1k6i4m8S2k6q4\)9J5k6r3#2V1i4K6u0W2M7s2V1%60.)  <br>hrtng的API枚举恢复列表literal.txt和apilist.txt(仅支持Windows)|
|[LazyIDA](https://bbs.kanxue.com/elink@9c4K9s2c8@1M7s2y4Q4x3@1q4Q4x3V1k6Q4x3V1k6Y4K9i4c8Z5N6h3u0Q4x3X3g2U0L8$3#2Q4x3V1k6x3y4s2W2K6i4K6u0r3e0r3q4*7P5f1W2p5b7b7%60.%60.)|快速转换提取数据|将LazyIDA.py复制到plugins目录|支持9.2  <br>注意convert标签改成了Dump|
|[auto-enum](https://bbs.kanxue.com/elink@22eK9s2c8@1M7s2y4Q4x3@1q4Q4x3V1k6Q4x3V1k6Y4K9i4c8Z5N6h3u0Q4x3X3g2U0L8$3#2Q4x3V1k6B7N6h3&6J5L8$3&6Q4x3V1k6S2N6i4c8G2i4K6u0V1k6h3&6#2L8b7%60.%60.)|自动恢复Windows和Linux的API参数枚举名|将plugin目录内的所有文件复制到ida/plugins下: enumlib, auto_enum.py, ida-plugin.json|支持9.2  <br>需在伪C界面右键点击Auto Enum使用|
|[bindiff](https://bbs.kanxue.com/elink@245K9s2c8@1M7s2y4Q4x3@1q4Q4x3V1k6Q4x3V1k6Y4K9i4c8Z5N6h3u0Q4x3X3g2U0L8$3#2Q4x3V1k6Y4L8$3!0Y4L8r3g2Q4x3V1k6T1K9h3&6V1K9h3k6X3)|函数相似度对比,常用于恢复符号|将binexport12_ida64.dll和bindiff8_ida64.dll复制到ida/plugins|不支持9.2  <br>适配IDA9的bindiff: https://bbs.kanxue.com/thread-283804.htm|

### 其他插件

|插件名|作用|安装方法|备注|
|---|---|---|---|
|[Ponce](https://bbs.kanxue.com/elink@cb6K9s2c8@1M7s2y4Q4x3@1q4Q4x3V1k6Q4x3V1k6Y4K9i4c8Z5N6h3u0Q4x3X3g2U0L8$3#2Q4x3V1k6A6L8r3I4W2M7X3p5^5z5q4\)9J5c8W2m8G2L8X3y4W2)|符号执行/污点分析插件,可用于爆破|将ponce.dll安装到plugins目录|不支持9.2  <br>适配9.1的ponce:https://github.com/copythere/Ponce, 经测试同样支持9.2|
|[deREferencing](https://bbs.kanxue.com/elink@392K9s2c8@1M7s2y4Q4x3@1q4Q4x3V1k6Q4x3V1k6Y4K9i4c8Z5N6h3u0Q4x3X3g2U0L8$3#2Q4x3V1k6V1j5h3&6A6k6$3q4J5k6%4g2Q4x3V1k6V1k6g2u0q4k6X3g2J5k6h3&6U0K9h3&6Y4)|调试时使用,追踪栈和寄存器指向的内容|将dereferencing.py和dereferencing文件夹复制到ida/plugins|效果有限,由于9.2优化了寄存器列表,只有调用栈试图相对有用|
|[D810](https://bbs.kanxue.com/elink@449K9s2c8@1M7s2y4Q4x3@1q4Q4x3V1k6Q4x3V1k6Y4K9i4c8D9j5h3u0Q4x3X3g2U0L8$3#2Q4x3V1k6W2M7$3S2S2M7X3c8Q4x3V1k6V1z5o6p5H3i4K6u0W2k6$3W2@1)|去除OLLVM混淆|使用前需要idapython安装z3  <br>"python -m pip install z3-solver"  <br>将d810文件夹和d810.py复制到plugins目录|安装了Hrtng则可以不安装该插件|
|[IDA Feeds](https://bbs.kanxue.com/elink@330K9s2c8@1M7s2y4Q4x3@1q4Q4x3V1k6Q4x3V1k6V1L8$3y4K6i4K6u0W2K9r3g2%5E5i4K6u0V1M7X3q4&6M7#2\)9J5k6h3y4G2L8g2\)9J5c8Y4g2K6k6i4u0Q4x3X3c8Y4N6h3W2V1k6g2\)9J5c8Y4m8D9N6h3N6A6L8Y4y4Q4x3V1k6H3L8s2g2Y4K9h3&6K6i4K6u0V1M7$3S2A6M7s2m8W2k6q4\)9J5k6s2N6A6N6r3S2Q4x3X3c8A6k6r3q4Q4x3V1k6A6k6r3q4Q4x3X3c8X3k6h3g2V1M7H3%60.%60.)|匹配部分常见库函数符号|参考IDA Pro 9.1部分|效果有限|
|[ida-pro-mcp](https://bbs.kanxue.com/elink@0dbK9s2c8@1M7s2y4Q4x3@1q4Q4x3V1k6Q4x3V1k6Y4K9i4c8Z5N6h3u0Q4x3X3g2U0L8$3#2Q4x3V1k6E0M7X3g2^5L8$3c8A6j5g2\)9J5c8X3W2V1j5g2\)9J5k6s2m8J5L8#2\)9J5k6r3#2U0M7l9%60.%60.)|在IDA中使用MCP服务|参考IDA Pro 9.1部分|和WPeChatGPT效果类似,但token消耗较大|
|[WPeChatGPT](https://bbs.kanxue.com/elink@e98K9s2c8@1M7s2y4Q4x3@1q4Q4x3V1k6Q4x3V1k6Y4K9i4c8Z5N6h3u0Q4x3X3g2U0L8$3#2Q4x3V1k6i4f1r3g2S2j5$3g2Q4x3X3c8t1j5@1S2Q4x3V1k6i4f1r3g2o6K9r3q4@1c8#2m8f1)|利用LLM辅助分析|参考IDA Pro 9.0部分|效果有限,仅供辅助|
|[IDA_ClassInformer_PlugIn](https://bbs.kanxue.com/elink@841K9s2c8@1M7s2y4Q4x3@1q4Q4x3V1k6Q4x3V1k6Y4K9i4c8Z5N6h3u0Q4x3X3g2U0L8$3#2Q4x3V1k6C8N6$3g2S2N6r3S2W2M7X3#2S2L8W2\)9J5c8V1W2p5b7g2\)9#2k6V1y4D9j5i4y4K6d9h3&6X3L8%4u0E0k6i4u0Q4y4h3k6b7L8s2g2Y4d9h3^5%60.)|反编译C++时, 可以根据RTTI等信息综合恢复类Class的相关信息，例如继承信息，类名等|将IDA_ClassInformer.dll复制到ida/plugins目录||
|[HexRaysCodeXplorer](https://bbs.kanxue.com/elink@2fdK9s2c8@1M7s2y4Q4x3@1q4Q4x3V1k6Q4x3V1k6%4N6%4N6Q4x3X3f1#2x3Y4m8G2K9X3W2W2i4K6u0W2j5$3&6Q4x3V1k6X3L8%4u0#2L8g2\)9J5k6i4m8Z5M7q4\)9K6c8X3#2G2k6q4\)9K6c8s2k6A6k6i4N6@1K9s2u0W2j5h3c8Q4x3U0k6S2L8i4m8Q4x3@1u0@1K9h3c8Q4x3@1b7I4z5e0V1&6z5e0l9#2i4K6t1$3j5h3#2H3i4K6y4n7K9r3W2Y4K9r3I4A6k6$3S2@1i4K6y4p5d9r3g2^5f1X3q4&6M7@1y4G2k6r3g2j5M7r3I4G2M7X3g2J5)|自动识别结构体，显示C++虚函数，生成函数结构树等|将HexRaysCodeXplorer64.dll复制到ida/plugins目录||

# IDA Pro 9.1.250226

## 前言

9.0 SP1还没捂热,就发布了9.1,相比之下9.1修了不少bug,分析程序更快更丝滑,还有signatures-bundle和IDA Feeds可以使用

实测9.0的patch脚本可用于9.1,并且大部分9.0的插件可用于9.1,由于二者配置方法类似便不多赘述

更新部分如下:

1. 初始化IDA
    
    参考Binwalker师傅编写的7.7绿色版的IDA_InitTool
    
    使用python实现禁用IDA自动更新和设置IDAPython路径的功能(默认使用嵌入的python3.11.9)
    
2. 配置和使用IDA Feeds插件
    
    泄露文件中包括了符号库signatures-bundles-9.1.zip,物尽其用配置了一波该插件
    
3. 配置和使用IDA MCP插件
    
    实测自动化分析效果和WPeChatGPT差不多,但能看到分析过程,需要注意消耗的token更多
    

提供配置好的IDA9.1压缩包,初次使用前运行InitIDA.exe后即可使用(WPeChatgpt需要手动配置api和模型)

IDA Professional 9.1.7z 链接: https://pan.baidu.com/s/16Hk9FjEygb1yohUzblxdFw?pwd=8put 提取码: 8put

**声明: 文章资源仅作学习交流使用，不得用于商业或者非法用途，请测试后尽快删除，购买正版进行支持**

## 初始化IDA

参考Binwalker师傅IDA7.7绿色版的IDA_InitTool.exe

功能为: 修改注册表,实现禁用自动更新和设置IDAPython路径;创建桌面快捷方式

使用pyinstaller打包为InitIDA.exe

|   |   |
|---|---|
|1<br><br>2<br><br>3<br><br>4<br><br>5<br><br>6<br><br>7<br><br>8<br><br>9<br><br>10<br><br>11<br><br>12<br><br>13<br><br>14<br><br>15<br><br>16<br><br>17<br><br>18<br><br>19<br><br>20<br><br>21<br><br>22<br><br>23<br><br>24<br><br>25<br><br>26<br><br>27<br><br>28<br><br>29<br><br>30<br><br>31<br><br>32<br><br>33<br><br>34<br><br>35<br><br>36<br><br>37<br><br>38<br><br>39<br><br>40<br><br>41<br><br>42<br><br>43<br><br>44<br><br>45<br><br>46<br><br>47<br><br>48<br><br>49<br><br>50<br><br>51<br><br>52<br><br>53<br><br>54<br><br>55<br><br>56<br><br>57<br><br>58<br><br>59<br><br>60<br><br>61<br><br>62<br><br>63<br><br>64<br><br>65<br><br>66<br><br>67<br><br>68<br><br>69<br><br>70<br><br>71<br><br>72<br><br>73<br><br>74<br><br>75<br><br>76<br><br>77<br><br>78<br><br>79<br><br>80<br><br>81<br><br>82<br><br>83<br><br>84<br><br>85<br><br>86<br><br>87<br><br>88<br><br>89<br><br>90<br><br>91<br><br>92<br><br>93<br><br>94<br><br>95<br><br>96<br><br>97|`import` `os`<br><br>`import` `winreg`<br><br>`import` `win32com.client`<br><br>`def` `set_ida_reg(py_dll_path):`<br><br>    `"""`<br><br>    `配置IDA注册表设置`<br><br>    `功能:禁用自动更新 + 设置Python路径`<br><br>    `"""`<br><br>    `try``:`<br><br>        `key_path` `=` `r``"SOFTWARE\Hex-Rays\IDA"`<br><br>        `key` `=` `winreg.CreateKey(winreg.HKEY_CURRENT_USER, key_path)`<br><br>        `with key:`<br><br>            `# 禁用自动更新功能`<br><br>            `winreg.SetValueEx(key,` `"AutoCheckUpdates"``,` `0``, winreg.REG_DWORD,` `0``)`<br><br>            `winreg.SetValueEx(key,` `"AutoRequestUpdates"``,` `0``, winreg.REG_DWORD,` `0``)`<br><br>            `winreg.SetValueEx(key,` `"AutoUseLumina"``,` `0``, winreg.REG_DWORD,` `0``)`<br><br>            `print``(``"Ban IDA AutoUpdate succeeded"``)`<br><br>            `# 配置IDA Python,由 HKEY_CURRENT_USER\SOFTWARE\Hex-Rays\IDA\Python3TargetDLL 指定`<br><br>            `if` `py_dll_path:`<br><br>                `winreg.SetValueEx(key,` `"Python3TargetDLL"``,` `0``, winreg.REG_SZ, py_dll_path)`<br><br>                `print``(``"Setting IDAPython Path succeeded"``)`<br><br>        `return` `True`<br><br>    `except` `Exception as e:`<br><br>        `print``(f``"注册表操作失败: {e}"``)`<br><br>        `return` `False`<br><br>`def` `create_shortcut(target):`<br><br>    `"""创建桌面快捷方式"""`<br><br>    `name``=``"IDA Pro 9.1"` `# 快捷方式名称`<br><br>    `desc``=``"The Interactive Disassembler"` `# 快捷方式描述`<br><br>    `try``:`<br><br>        `desktop` `=` `os.path.join(os.path.expanduser(``"~"``),` `"Desktop"``)`<br><br>        `shortcut_path` `=` `os.path.join(desktop, f``"{name}.lnk"``)`<br><br>        `shell` `=` `win32com.client.Dispatch(``"WScript.Shell"``)`<br><br>        `shortcut` `=` `shell.CreateShortcut(shortcut_path)`<br><br>        `shortcut.TargetPath` `=` `target`<br><br>        `shortcut.WorkingDirectory` `=` `os.path.dirname(target)`<br><br>        `shortcut.Description` `=` `desc`<br><br>        `shortcut.Save()`<br><br>        `print``(``"Create shortcut succeeded"``)`<br><br>    `except` `Exception as e:`<br><br>        `print``(``"Create shortcut failed: "``, e)`<br><br>`def` `check_python_env(py_dir):`<br><br>    `py_dll` `=` `os.path.join(py_dir,` `"python3.dll"``)`<br><br>    `if` `os.path.isdir(py_dir)` `=``=` `False``:`<br><br>        `print``(``"\nError: embedded python directory not found!"``)`<br><br>        `return` `False`<br><br>    `if` `os.path.isfile(py_dll)` `=``=` `False``:`<br><br>        `print``(``"\nError: embedded python3.dll not found!"``)`<br><br>        `return` `False`<br><br>    `return` `True`<br><br>`def` `main():`<br><br>    `# 打印程序标题`<br><br>    `print``(``"============================================================================================"``)`<br><br>    `print``(``"       IDA Initilizer created by OrientalGlass (Refer to Binwalker's IDA_InitTool)"``)`<br><br>    `print``(``"============================================================================================"``)`<br><br>    `# 构建路径配置`<br><br>    `cwd` `=` `os.getcwd()`<br><br>    `ida_path` `=` `os.path.join(cwd,` `"ida.exe"``)`          `# IDA主程序`<br><br>    `py_dir` `=` `os.path.join(cwd,` `"python311"``)`          `# Python目录`<br><br>    `py_dll` `=` `os.path.join(py_dir,` `"python3.dll"``)`      `# Python DLL文件`<br><br>    `# 检测IDA路径`<br><br>    `if` `os.path.exists(ida_path)` `=``=``False``:`<br><br>        `print``(``"Error: please run this script in IDA directory"``)`<br><br>        `return`<br><br>    `else``:`<br><br>        `print``(f``"IDA Path: {ida_path}"``)`<br><br>    `# 主配置流程`<br><br>    `print``(``"\n------------------------------------------------------------"``)`<br><br>    `choice` `=` `input``(``"\nUse default initialization settings?(Y/N y/n): "``).lower()`<br><br>    `choice_yes_items``=``('``','``y``','``Y``','``yes')` `# 确定选项,含默认`<br><br>    `if` `choice` `in` `choice_yes_items` `and` `check_python_env(py_dir):`<br><br>        `# 默认配置模式`<br><br>        `set_ida_reg(py_dll)`<br><br>        `create_shortcut(ida_path)`<br><br>    `else``:`<br><br>        `# 手动配置模式`<br><br>        `py_choice` `=` `input``(``"\nUse embedded idapython?(Y/N y/n): "``).lower()`<br><br>        `if` `py_choice` `in` `choice_yes_items` `and` `check_python_env(py_dir):`<br><br>            `set_ida_reg(py_dll)`<br><br>        `sc_choice` `=` `input``(``"\nCreate desktop shortcut?(Y/N y/n): "``).lower()`<br><br>        `if` `sc_choice` `in` `choice_yes_items:`<br><br>            `create_shortcut(ida_path)`<br><br>`if` `__name__` `=``=` `"__main__"``:`<br><br>    `main()`|

运行效果如下

![](https://bbs.kanxue.com/upload/attach/202509/968342_2DJ7X8D5647GFE3.png)

如果只需要修改IDAPython可简化脚本

|   |   |
|---|---|
|1<br><br>2<br><br>3<br><br>4<br><br>5<br><br>6<br><br>7<br><br>8<br><br>9<br><br>10<br><br>11<br><br>12<br><br>13<br><br>14<br><br>15<br><br>16<br><br>17<br><br>18<br><br>19<br><br>20<br><br>21<br><br>22<br><br>23<br><br>24<br><br>25<br><br>26<br><br>27<br><br>28<br><br>29<br><br>30<br><br>31<br><br>32<br><br>33<br><br>34<br><br>35<br><br>36<br><br>37<br><br>38<br><br>39<br><br>40<br><br>41<br><br>42<br><br>43<br><br>44<br><br>45<br><br>46<br><br>47<br><br>48<br><br>49<br><br>50<br><br>51<br><br>52<br><br>53<br><br>54|`import` `os`<br><br>`import` `winreg`<br><br>`def` `set_ida_reg(py_dll_path):`<br><br>    `"""`<br><br>    `功能:设置Python路径`<br><br>    `"""`<br><br>    `try``:`<br><br>        `key_path` `=` `r``"SOFTWARE\Hex-Rays\IDA"`<br><br>        `key` `=` `winreg.CreateKey(winreg.HKEY_CURRENT_USER, key_path)`<br><br>        `with key:`<br><br>            `# 配置IDA Python,由 HKEY_CURRENT_USER\SOFTWARE\Hex-Rays\IDA\Python3TargetDLL 指定`<br><br>            `if` `py_dll_path:`<br><br>                `winreg.SetValueEx(key,` `"Python3TargetDLL"``,` `0``, winreg.REG_SZ, py_dll_path)`<br><br>                `print``(``"Setting IDAPython Path succeeded"``)`<br><br>        `return` `True`<br><br>    `except` `Exception as e:`<br><br>        `print``(f``"注册表操作失败: {e}"``)`<br><br>        `return` `False`<br><br>`def` `check_python_env(py_dir):`<br><br>    `py_dll` `=` `os.path.join(py_dir,` `"python3.dll"``)`<br><br>    `if` `os.path.isdir(py_dir)` `=``=` `False``:`<br><br>        `print``(``"\nError: embedded python directory not found!"``)`<br><br>        `return` `False`<br><br>    `if` `os.path.isfile(py_dll)` `=``=` `False``:`<br><br>        `print``(``"\nError: embedded python3.dll not found!"``)`<br><br>        `return` `False`<br><br>    `return` `True`<br><br>`def` `main():`<br><br>    `# 打印程序标题`<br><br>    `print``(``"======================================="``)`<br><br>    `print``(``"=====IDA Python Environment Setup======"``)`<br><br>    `print``(``"======================================="``)`<br><br>    `# 构建路径配置`<br><br>    `cwd` `=` `os.getcwd()`<br><br>    `ida_path` `=` `os.path.join(cwd,` `"ida.exe"``)`          `# IDA主程序`<br><br>    `py_dir` `=` `os.path.join(cwd,` `"python311"``)`          `# Python目录`<br><br>    `py_dll` `=` `os.path.join(py_dir,` `"python3.dll"``)`      `# Python DLL文件`<br><br>    `# 检测IDA路径`<br><br>    `if` `os.path.exists(ida_path)` `=``=``False``:`<br><br>        `print``(``"Error: please run this script in IDA directory"``)`<br><br>        `return`<br><br>    `else``:`<br><br>        `print``(f``"IDA Path: {ida_path}"``)`<br><br>    `if` `check_python_env(py_dir):`<br><br>        `# 默认配置模式`<br><br>        `set_ida_reg(py_dll)`<br><br>`if` `__name__` `=``=` `"__main__"``:`<br><br>    `main()`|

## IDA Feeds

详情参考官网[IDA Feeds](https://bbs.kanxue.com/elink@a6cK9s2c8@1M7s2y4Q4x3@1q4Q4x3V1k6Q4x3V1k6V1L8$3y4K6i4K6u0W2K9r3g2%5E5i4K6u0V1M7X3q4&6M7#2\)9J5k6h3y4G2L8g2\)9J5c8Y4g2K6k6i4u0Q4x3X3c8Y4N6h3W2V1k6g2\)9J5c8Y4m8D9N6h3N6A6L8Y4y4Q4x3V1k6H3L8s2g2Y4K9h3&6K6i4K6u0V1M7$3S2A6M7s2m8W2k6q4\)9J5k6s2N6A6N6r3S2Q4x3X3c8A6k6r3q4Q4x3V1k6A6k6r3q4Q4x3X3c8X3k6h3g2V1M7H3%60.%60.)

### 安装依赖

基本使用只能顺序扫描,完全使用支持并行扫描,需要配置以下依赖:

- idalib
- RPyc5.x 用于并行探测
- ida_feeds/config.json的flair路径

具体步骤:

1. 首先使用idapython安装和激活idalib
    
    使用idapython,指定pip下载idalib/python目录下setup.py指定的内容
    
    python -m pip install ../idalib/python/. # 安装idalib
    python ../idalib/python/py-activate-idalib.py # 激活idalib
    
    ![IDA-Feeds-下载idalib](https://bbs.kanxue.com/upload/attach/202509/968342_MTQMK784RKRQMZY.png)
    
    ![](https://bbs.kanxue.com/upload/attach/202509/968342_Y3J92E4H44BMKN3.png)
    
2. 下载idafeeds的依赖(RPyc)
    
    python -m pip install -r ../plugins/ida_feeds/requirements.txt
    
    requirements.txt:
    
    |   |   |
    |---|---|
    |1<br><br>2<br><br>3<br><br>4<br><br>5|`PyQt5``=``=``5.15``.``11`<br><br>`PyQt5_sip``=``=``12.15``.``0`<br><br>`Requests``=``=``2.32``.``3`<br><br>`rpyc``=``=``6.0``.``1`<br><br>`tomli``=``=``2.2``.``1`|
    
    ![](https://bbs.kanxue.com/upload/attach/202509/968342_EWDJXNF2SKGW5JG.png)
    
3. 配置ida_feeds/config.json的flair路径
    
    修改config.sample.json并复制一份命名为config.json即可
    
    ![](https://bbs.kanxue.com/upload/attach/202509/968342_QRS59Z7MBTMHXC7.png)
    

### 使用IDA Feeds

下载并解压signatures-bundles-9.1.zip后,将文件夹内的子文件夹符号库复制到~\IDA Professional 9.1\sig文件夹下即可

插件在Edit>plugins>IDA Feeds启动

![IDA-Feeds启动插件](https://bbs.kanxue.com/upload/attach/202509/968342_7G5M5NX5JPNZH3N.png)

使用步骤:

1. 先选择指定符号库,再选择扫描模式
    
2. 选中符号库的某个符号文件,按ctrl+a选中所有符号,再点击运行探测
    
3. 按住ctrl,选中所有匹配到的签名,点击Apply signatures
    

![](https://bbs.kanxue.com/upload/attach/202509/968342_4CDPVXWA6G7NFUE.png)

符号恢复效果如下,能恢复很多常见库函数符号

![IDA-Feeds-符号恢复效果](https://bbs.kanxue.com/upload/attach/202509/968342_SZUC74BAYS52PVW.png)

## IDA MCP

参考

[[分享]基于mcp-server实现的ida自动化分析](https://bbs.kanxue.com/thread-286425.htm#msg_header_h2_1)

https://github.com/mrexodia/ida-pro-mcp

### 配置VSCode Cline

能连接或者探测到本地mcp server的任意插件均可

到VSCode的插件商城安装Cline插件后,配置模型和API,可选择自动授权

![](https://bbs.kanxue.com/upload/attach/202509/968342_AF4UVDQKVYZKA7F.png)

### 安装IDA MCP Server

首先使用idapython下载ida-pro-mcp程序(注意不要和系统python混淆)

python -m pip install --upgrade git+https://github.com/mrexodia/ida-pro-mcp

![](https://bbs.kanxue.com/upload/attach/202509/968342_EPN69MDXBFZU8TF.png)

之后进入IDAPython的Scripts目录运行ida-pro-mcp.exe(若IDAPython不为系统python则需要手动进入该目录运行)

需要先安装对应插件(如Cline),再运行ida-pro-mcp,否则不会生成配置文件

![](https://bbs.kanxue.com/upload/attach/202509/968342_75DABTBY47JKKCV.png)

成功生成配置文件后,到IDA中运行MCP-Server

![IDA-MCP-ida-启动mcp-server](https://bbs.kanxue.com/upload/attach/202509/968342_PEPX4E3XXP3UFDT.png)

如果Cline能检测到server则配置成功

![IDA-MCP-Servers](https://bbs.kanxue.com/upload/attach/202509/968342_R3YWU6U9V233PPD.png)

之后提问进行自动化分析

![](https://bbs.kanxue.com/upload/attach/202509/968342_KYCZKTZR2YPTKGB.png)

和WPeChatgpt分析结果对比

![](https://bbs.kanxue.com/upload/attach/202509/968342_8ZK3J3JSWCJCR58.png)

### 问题: git拉取失败

解决办法: 使用**git congig --global --get http.proxy**查询网络代理,设置本地代理后即可成功拉取

报错如下:

E:\Tools\BinaryTools\Disassemblers\IDA Professional 9.1\python311>python -m pip install --upgrade git+https://github.com/mrexodia/ida-pro-mcp
Collecting git+https://github.com/mrexodia/ida-pro-mcp
  Cloning https://github.com/mrexodia/ida-pro-mcp to c:\users\admin\appdata\local\temp\pip-req-build-fk05eysp
  Running command git clone --filter=blob:none --quiet https://github.com/mrexodia/ida-pro-mcp 'C:\Users\admin\AppData\Local\Temp\pip-req-build-fk05eysp'
  fatal: unable to access 'https://github.com/mrexodia/ida-pro-mcp/': Failed to connect to github.com port 443 after 21156 ms: Couldn't connect to server
  error: subprocess-exited-with-error

  × git clone --filter=blob:none --quiet https://github.com/mrexodia/ida-pro-mcp 'C:\Users\admin\AppData\Local\Temp\pip-req-build-fk05eysp' did not run successfully.
  │ exit code: 128
  ╰─> See above for output.

  note: This error originates from a subprocess, and is likely not a problem with pip.
error: subprocess-exited-with-error

× git clone --filter=blob:none --quiet https://github.com/mrexodia/ida-pro-mcp 'C:\Users\admin\AppData\Local\Temp\pip-req-build-fk05eysp' did not run successfully.
│ exit code: 128
╰─> See above for output.

note: This error originates from a subprocess, and is likely not a problem with pip.

## 配置优化

参考[IDA Pro 7.7.220118 (SP1) 全插件绿色版](https://bbs.kanxue.com/elink@bdeK9s2c8@1M7s2y4Q4x3@1q4Q4x3V1k6Q4x3V1k6%4N6%4N6Q4x3X3f1#2x3Y4m8G2K9X3W2W2i4K6u0W2j5$3&6Q4x3V1k6X3L8%4u0#2L8g2\)9J5k6i4m8Z5M7q4\)9K6c8X3#2G2k6q4\)9K6c8s2k6A6k6i4N6@1K9s2u0W2j5h3c8Q4x3U0k6S2L8i4m8Q4x3@1u0@1K9h3c8Q4x3@1b7I4y4e0R3@1x3e0p5#2i4K6t1$3j5h3#2H3i4K6y4n7K9r3W2Y4K9r3I4A6k6$3S2@1i4K6y4p5K9h3c8S2i4K6t1#2x3V1t1%4i4K6u0W2y4H3%60.%60.)

cfg/ida.cfg

|   |   |
|---|---|
|1<br><br>2<br><br>3<br><br>4<br><br>5<br><br>6<br><br>7<br><br>8|`STORE_USER_INFO` `=` `YES` `-``> NO` `/``/` `关闭idb的用户信息`<br><br>`OPCODE_BYTES` `=` `0` `-``>` `10`       `/``/` `反汇编界面显示``10``字节指令硬编码`<br><br>`INDENTION` `=` `16` `-``>` `0`      `/``/` `硬编码和汇编指令的间距`<br><br>`SHOW_BASIC_BLOCKS` `=` `NO` `-``> YES`    `/``/``在基本块的末尾生成一个空行`<br><br>`SHOW_XREFS` `=` `2` `-``>` `16`             `/``/``交叉引用显示数`<br><br>`SHOW_SOURCE_LINNUM`  `=` `NO` `-``> YES` `/``/``显示源码行号`<br><br>`SHOW_SP` `=` `NO` `-``> YES`          `/``/``显示SP指针偏移`<br><br>`ENCODING_CULTURES 添加 GB2312: Chinese` `/``/``暂不清楚作用`|

cfg/Chinese.clt

|   |   |
|---|---|
|1<br><br>2<br><br>3|`增加(暂不清楚作用):`<br><br>`u2000..u206F,`<br><br>`u3000..u303F,`|

# IDA Pro 9.0.241217 SP1

## 前言

使用了许久的ida7.7想更新到ida9,虽然成功安装并patch但IDAPython环境和插件没有配置好用起来不顺手

本文简单介绍IDA Pro 9.0.241217 SP1的安装步骤,IDAPython的配置,以及常用插件的地址和安装方法

打包了配置好的IDA9 SP1,设置IDAPython路径即可使用,使用方法文末简介

附件:

- IDAPlugins.zip
    
- IdaPro9Beta-Keygen-iRabbit.py
    
- IDA Professional 9.0.7z
    
    链接: https://pan.baidu.com/s/1eCmxbP6nNHm5qz41rFbetg?pwd=5hdq
    

## IDA9 SP1 安装

地址[[Disassemblers]**IDA Pro 9.0.241217 SP1**](https://bbs.kanxue.com/elink@28cK9s2c8@1M7s2y4Q4x3@1q4Q4x3V1k6Q4x3V1k6%4N6%4N6Q4x3X3f1#2x3Y4m8G2K9X3W2W2i4K6u0W2j5$3&6Q4x3V1k6@1K9s2u0W2j5h3c8Q4x3X3b7I4z5e0V1&6z5o6j5$3i4K6u0V1x3g2\)9J5k6o6q4Q4x3X3g2Z5N6r3#2D9)

参考如下步骤

1. 运行ida-pro_90sp1_x64win.exe安装ida
2. 修改IdaPro9Beta-Keygen-iRabbit.py文件的部分内容,复制到ida根目录
3. python运行keygen,自动修补
4. 修改patched文件后缀,替换ida.dll和ida32.dll(注意保存原始文件)

![IDA9-patch](https://bbs.kanxue.com/upload/attach/202509/968342_NG5BNAKXJKGHHJX.png)

keygen修补成功输出如下,windows平台patch ida.dll和ida32.dll

![](https://bbs.kanxue.com/upload/attach/202509/968342_NXYYHJNK5FYYRSK.png)

## 优化设置

### 使用经典快捷键

ida9的新快捷键用起来不习惯, 可在options>shortcuts,取消勾选use new shortcuts使用老快捷键

![](https://bbs.kanxue.com/upload/attach/202509/968342_6YFZDHS437AWAVM.png)

### 开启操作码显示

options>general>Number of opcode bytes, 输入10在大部分情况下够用

![](https://bbs.kanxue.com/upload/attach/202509/968342_T7J5Y2UGYZSSTZ5.png)

## 插件安装

灵感来源[IDA 9.0.20241216 (SP1)安装教程](https://bbs.kanxue.com/thread-285604.htm) 由于不想交钱故自己折腾

### IDAPython

大部分插件的运行依赖于IDAPython环境,而IDAPython并不神秘,使用官方的Python解释器即可

python目录内是idapython脚本相关模块

![](https://bbs.kanxue.com/upload/attach/202509/968342_9TQKG57686NBSCC.png)

PyQt5文件夹内可以发现不同python版本的库(ida插件图形化)

所以ida9的python版本需要在3.8-3.13之间(推荐3.10和3.11)

![](https://bbs.kanxue.com/upload/attach/202509/968342_4JF3X8QP7USSYRY.png)

最初我直接使用ida7.7绿色版的python3.8,大部分插件仍然可以运行,但findcrypt报错

网上冲浪听说ida9使用python 3.11更稳定,故安装该版本,下载后直接运行即可

https://www.python.org/ftp/python/3.11.9/python-3.11.9-amd64.exe

为方便使用我安装到了IDA根目录内并命名为python311(不需要添加到环境变量)

![](https://bbs.kanxue.com/upload/attach/202509/968342_XHW7RPS33NYJTZS.png)

安装完python后,需要手动设置idapython路径,运行ida根目录的idapyswitch即可

|   |   |
|---|---|
|1|`idapyswitch.exe` `-``-``force``-``path .``/``python311``/``python3.dll`|

可以参考[IDA Pro 切换 Python 版本](https://bbs.kanxue.com/elink@d48K9s2c8@1M7s2y4Q4x3@1q4Q4x3V1k6Q4x3V1k6T1L8r3!0Y4i4K6u0W2j5%4y4V1L8W2\)9J5k6h3&6W2N6q4\)9J5c8Y4q4I4i4K6g2X3x3U0p5H3y4U0x3%5E5y4K6y4Q4x3V1k6S2M7Y4c8A6j5$3I4W2i4K6u0r3k6r3g2@1j5h3W2D9M7#2\)9J5c8U0p5@1x3K6x3%4x3o6l9@1x3l9%60.%60.)

|   |   |
|---|---|
|1<br><br>2<br><br>3<br><br>4<br><br>5|`保存依赖`<br><br>`python.exe` `-``m pip freeze > requirements.txt`<br><br>`下载依赖`<br><br>`python.exe` `-``m pip install` `-``r requirements.txt`|

### Plugins

以下为插件名及其功能介绍

|插件|功能|
|---|---|
|**LazyIDA**|convert快速提取数据等|
|**Keypatch**|patch指令方便|
|**Patching**|patch16进制数据方便|
|**findcrypt-yara**|常见加密算法识别|
|**auto-enum**|自动恢复常见api的枚举变量|
|**Hrtng**|高亮括号,重定义关键函数声明,栈字符串识别,反ollvm等功能|
|D810|去ollvm混淆脚本,安装Hrtng后可不安装该插件|
|classinformer|反编译C++时, 可以根据RTTI等信息综合恢复类Class的相关信息，例如继承信息，类名等。|
|**deREferencing**|调试时使用,追踪栈和寄存器指向的内容|
|HexRaysCodeXplorer|自动识别结构体，显示C++虚函数，生成函数结构树等|
|**DataExportPlus**|提取数据增强版|
|**bindiff**|符号恢复|
|**WPeChatGPT**|AI大语言模型插件,接入api后可自动分析函数和程序|

下面简介各插件的地址,功能,安装方法

### LazyIDA

https://github.com/L4ys/LazyIDA

将LazyIDA.py复制到plugins目录下即可

### Keypatch

使用前需要安装keystone-engine和six模块(py3.11自带six无需额外安装)

|   |   |
|---|---|
|1<br><br>2|`python` `-``m pip install keystone``-``engine`<br><br>`python` `-``m pip install six`|

注意: 是keystone-engine不是keystone

项目地址: https://github.com/keystone-engine/keypatch

适配IDA9的keypatch: https://bbs.kanxue.com/thread-282852.htm

将Keypatch.py复制到plugins目录下即可

### Patching

https://github.com/gaasedelen/patching

将Patching文件夹和Patching.py复制到plugins目录下即可

### findcrypt-yara

使用前需要idapython安装yara-pyhon(注意不是yara)

|   |   |
|---|---|
|1|`python` `-``m pip install yara``-``python`|

地址: https://github.com/polymorf/findcrypt-yara

将findcrypt3.py和findcrypt3.rules复制到ida/plugins目录下即可

注意: 该插件在python3.8环境下无法运行

### D810

去除OLLVM混淆,如果安装了Hrtng可以不安装该插件

使用前需要idapython安装z3

|   |   |
|---|---|
|1|`python` `-``m pip install z3``-``solver`|

下载地址

|   |   |
|---|---|
|1|`git clone https:``/``/``gitlab.com``/``eshard``/``d810.git`|

将d810文件夹和d810.py复制到plugins目录下即可

### auto-enum

自动恢复常见函数的枚举

https://github.com/junron/auto-enum

下载后将项目plugin目录内的所有文件:

- enumlib
    
- auto_enum.py
    
- ida-plugin.json
    

复制到ida/plugins下即可

### Hrtng

高亮括号,重定义关键函数声明,栈字符串识别,反ollvm等功能

https://github.com/KasperskyLab/hrtng

下载release包后解压,复制plugins/windows/9.0/hrtng.dll到ida/plugins目录下即可

### classinformer

https://github.com/herosi/classinformer

反编译C++时, 可以根据RTTI等信息综合恢复类Class的相关信息，例如继承信息，类名等。

下载release包后将Classinformer64.dll复制到ida/plugins目录下即可

### deREferencing

https://github.com/danigargu/deREferencing

调试时使用,追踪栈和寄存器指向的内容

将dereferencing.py和dereferencing文件夹复制到ida/plugins

### HexRaysCodeXplorer

自动识别结构体，显示C++虚函数，生成函数结构树等

https://www.52pojie.cn/forum.php?mod=viewthread&tid=1999905&highlight=HexRaysCodeXplorer

### DataExportPlus

https://github.com/Krietz7/IDA-DataExportPlus

shift+e 数据提取强化版,将DataExportPlus.py复制到plugins目录下即可

### findhash

项目地址https://github.com/Pr0214/findhash

该插件可以搜索出被魔改的哈希算法

把findhash.xml和findhash.py复制到plugins目录下即可

## WPeChatGPT

项目地址 https://github.com/WPeace-HcH/WPeChatGPT 该项目基于**[Gepetto](https://bbs.kanxue.com/elink@22aK9s2c8@1M7s2y4Q4x3@1q4Q4x3V1k6Q4x3V1k6Y4K9i4c8Z5N6h3u0Q4x3X3g2U0L8$3#2Q4x3V1k6v1N6i4y4@1K9h3y4W2f1X3q4Y4k6g2\)9J5c8V1N6W2M7r3g2@1N6r3\)9%60.)**

### 安装和使用插件

1. 安装插件依赖
    
    |   |   |
    |---|---|
    |1|`python -m pip` `install` `-r ~\WPeChatGPT-main\requirements.txt`|
    
    依赖文件requirements.txt内容如下
    
    |   |   |
    |---|---|
    |1<br><br>2<br><br>3|`openai >``=` `0.27``.``0`<br><br>`anytree`<br><br>`httpx`|
    
2. 修改WPeChatGPT.py
    
    默认支持OpenAI和DeepSeek模型,修改PLUGIN_NAME和model_api_key即可切换模型
    
    由于OpenAI API不易申请,DeepSeek关闭了申请渠道,故使用火山引擎的API(后文介绍)
    
    使用其他模型需要手动添加以下两个elif分支(根据自己的模型设置)
    
    |   |   |
    |---|---|
    |1|`client` `=` `openai.OpenAI(base_url` `=` `"https://ark.cn-beijing.volces.com/api/v3"``,api_key` `=` `model_api_key)`|
    
    ![](https://bbs.kanxue.com/upload/attach/202509/968342_RWSXZCJJVDDJY8H.png)
    
3. 复制WPeChatGPT.py和Auto-WPeGPT_WPeace到ida/plugins
    
    使用效果如下
    
    ![](https://bbs.kanxue.com/upload/attach/202509/968342_5B59995YYK9SNTZ.png)
    

### 申请API

该插件使用OpenAI SDK,默认支持OpenAI和DeepSeek模型,使用前需要申请api

推荐火山引擎,每个模型送50万免费token https://www.volcengine.com, 使用时注意token用量,扣钱了阿giao连蛋都不给你补

模型广场中,选择需要的模型,点击立即体验

![模型广场](https://bbs.kanxue.com/upload/attach/202509/968342_H2CYU7VATWEFFQ3.png)

立即体验默认提供GUI界面,选择API接入

![API接入](https://bbs.kanxue.com/upload/attach/202509/968342_ZBMRXR7PGCKNR9B.png)

创建API Key,名称任意,创建后复制并保存API Key,后续使用模型依赖该Key(**注意不要泄露**)

![APIKey](https://bbs.kanxue.com/upload/attach/202509/968342_2GWEUK3FTC4E77E.png)

之后选择自定义推理接入点>创建推理接入点

![创建推理接入点](https://bbs.kanxue.com/upload/attach/202509/968342_F4BY5SFQ274TDU9.png)

自行设置接入点名称,模型,确认接入

![](https://bbs.kanxue.com/upload/attach/202509/968342_Z4GESXA67M9YX3T.png)

选择模型

![选择模型](https://bbs.kanxue.com/upload/attach/202509/968342_XASYBYH26JCHU5G.png)

创建好后复制模型id和之前的API Key

![模型id](https://bbs.kanxue.com/upload/attach/202509/968342_7TKG59EXZHQFJ3N.png)

填充model_api_key和MODEL后,重启IDA即可使用插件

![](https://bbs.kanxue.com/upload/attach/202509/968342_H6NKQBC57555YY8.png)

## 问题-bindiff(已解决)

下载地址[[下载]bindiff_binexport for windows](https://bbs.kanxue.com/thread-283804.htm)

将binexport12_ida64.dll和bindiff8_ida64.dll复制到ida/plugins

或C:\Users\用户名\AppData\Roaming\Hex-Rays\IDA Pro\plugins下即可

同时支持32和64位样本

问题描述: 报错如下

![](https://bbs.kanxue.com/upload/attach/202509/968342_ZYDJ579PNRS4N2S.png)

推测是该路径为ida默认的设置路径,ida9.0和ida7.7的设置发生了冲突

备份保存一份7.7的IDA Pro设置后,删除C:\Users\admin\AppData\Roaming\Hex-Rays\IDA Pro\plugins下的文件即可解决报错

但是支持IDA9 SP1的插件没有找到,只有适用于RC1的:https://github.com/zhefox/Bindiff_for_IDA9.0

如果大佬们有适用于SP1的bindiff麻烦分享一下

## 直装

解压IDA Professional 9.0.7z后,运行根目录的idapyswitch设置idapython路径即可使用

|   |   |
|---|---|
|1|`idapyswitch.exe` `-``-``force``-``path .``/``python311``/``python3.dll`|

首次打开文件时,会询问是否使用新快捷键,选择No

![RevisedShortcut](https://bbs.kanxue.com/upload/attach/202509/968342_NQMYPUKCZU65CYQ.png)

之后弹出许可证协议,选择Agree

![LicenseAgreement](https://bbs.kanxue.com/upload/attach/202509/968342_YHGF8YPH4GJK6FS.png)

连接ida server更新,直接点ok

![](https://bbs.kanxue.com/upload/attach/202509/968342_RQCGQ7V4PQGNSS2.png)