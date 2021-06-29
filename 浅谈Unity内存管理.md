## 浅谈Unity内存管理

### 什么是内存？

> 物理内存、虚拟内存、内存寻址范围
>
> **物理内存：** 

### Android内存管理

> **内存基本单位 Page：** 4K一个Page，回收和分配以Page为单位。
>
> **内存杀手 low memory killer：** 
>
> **内存指标 *SS：** RSS（当前应用使用所有的内存，包括所有公共内存）、PSS（当前应用使用所有的内存，平摊公共内存）、USS（当前应用使用所有的内存，不包括公共内存）。使用 `procrank` 命令查看。

### Unity内存管理

> Unity内存按照分配方式分为：Native Memory、Managed Memory、Editor & Runtime。
>
> Unity内存按照管理方式分为：引擎管理内存、用户管理内存。
>
> Unity检测不到的内存：用户分配的native内存（如：插件、Lua）。
>
> Unity Native Memory管理：会及时返还给系统。Scene、Audio、Code Size、AssetBundle、Resoures文件夹、Texture、Mesh、Asset。
>
> Unity Managed Memory管理：
>
> VM内存池
>
> CG机制：回收能力、暂停时间、碎片化、额外消耗、可扩展性、可移植性。不分代、非压缩
