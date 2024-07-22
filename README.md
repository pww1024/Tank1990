# tank迁移配置流程记录

## 依赖

vs2019,win11

[Visual Studio工程实践开发(C++)](https://www.bilibili.com/video/BV1S541137P2)

[Tank1990源代码](https://github.com/krystiankaluzny/Tanks)

### 1.组织解决方案管理器文件结构

(0)解决方案 > 项目 > 筛选器(文件夹) > 项(文件)
(1)新建静态库类别项目
(2)项目设置不使用预编译头,所有配置
(3)*.h,*.cpp快速筛选添加现有项
(4)生成解决方案
(5)项目属性 -> C/C++ -> 常规 -> 附加包含目录 (C1083)，给每个项目附加$SolutionDir路径
(6)tank项目中添加引用,app_state,engine,objects打勾

### 2.使用外部库

(0)LNK2019无法解析的外部符号
(1)将外部库中的include更名为SDL2，把SDL2和lib一起拷贝到解决方案目录中
(2)在主程序项目中,tank属性->链接器->常规->添加库目录 $(SolutionDir)/lib/x86
(3)tank属性->链接器->输入->附加依赖项 添加lib文件夹目录中的*.lib文件,导入库
(4)正常生成,运行,但找不到*.dll
(5)拷贝dll文件到exe文件目录后运行,黑屏

### 3.运行不正常,资源缺失

(1)更改每个项目属性的调试页的工作目录为$(TargetDir)
(2)f5调试程序,阅读代码
(3)右键查找所有引用
(3)修改appconfig.cpp文件中的路径
(4)ctrl开火
