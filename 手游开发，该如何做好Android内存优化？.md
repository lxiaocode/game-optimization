## 手游开发，该如何做好Android内存优化？

https://mp.weixin.qq.com/s/t194bj5K5d5NluHrAYNfeg

### 认知

> **测不准：** 优化要做的第一件事就是测量。不要担心数据的准确性，因为测试过程中难免有误差，测试结果也会有一定的浮动，衡量Android内存的一些指标本身就不是一个精确值。
>
> **三个误区：** 
>
> 转场景内存有增量：Android或IOS为了流畅性，会将数据放入缓存中，并不会即使清理。只要保证Unity Profiler里看到Texture、Mesh、SerializedFile(AssetBundle)等常见易泄露的资源卸载干净即可。
>
> 一段时间内存一直增长：
>
> 进场场景Unity Profiler回落正常，但Android内存没有完全回落：Android内存包含了部分缓存，因此内存没有完全回落不能说明内存泄漏。

### 思维导图

![图片](https://mmbiz.qpic.cn/mmbiz_png/F03VdOKPlCkiaRKWADQWSQyeVvxFlyHdOV4xh57T76kNovMfyeVNlOgXbPicABjwmoeM48KoAvBsfUh1lLgTEfIQ/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

### 指标

> **指标主要有这些特征：** 易测量、符合逻辑、每次测量结果稳定。
>
> **常见指标：** USS、PSS、RSS、VSS。一般选择PSS作为指标。

#### 工具

> **dumpsys meminfo：** 主要用于测量PSS。
>
> **用法：** 
>
> ```shell
> adb shell dumpsys meminfo --package [包名]
> ```
>
> TODO：各个字段含义。

#### 主要内存消耗

> Android内存中主要消耗在：Native、Gfx、Unknown。
>
> **Native：** C/C++分配的内存，对于Unity而言是Unity引擎申请的内存。Native内存一个常见的问题是纹理开了Read/Write Enable，当纹理开启可读写后就会在Native内存中也存在一份。
>
> **显存：** Android的显存分为Gfx、GL两部分。（1）Gfx是指用户态显存，包含贴图、Mesh，使用Unity Memory Profiler可以查看。（2）GL是指内核态显存，包含Texture、Vertex Buffer等，但是GL指标很多设备不会显示。
>
> **Unknown：** 一般为Mono堆内存、Lua内存。Mono内存使用Unity Memory Profiler可以查看。

#### 次要内存消耗

>次要消耗在：Dalvik、EGL。
>
>**Dalvik：** Java虚拟机使用的堆内存，一般由Java申请。
>
>**EGL：** ...
