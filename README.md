# Draw  a Triangle

- ### 初始设置

  - Instance实例

    创建实例初始化vulkan库。实例是连接应用和库的。创建时需要把应用的信息传递给驱动。

    结构体来传递参数

  - 验证层 (validation layer

    验证层中的常见作用包括：

    - Checking the values of parameters against the specification to detect misuse
      根据规范检查参数值以检测误用
    - Tracking creation and destruction of objects to find resource leaks
      跟踪对象的创建和销毁以查找资源泄漏
    - Checking thread safety by tracking the threads that calls originate from
      通过跟踪调用源自
    - Logging every call and its parameters to the standard output
      将每个调用及其参数记录到标准输出中
    - Tracing Vulkan calls for profiling and replaying
      跟踪 Vulkan 需要进行分析和重放

    **TODO：这里跳过了消息回调**

  - 物理设备（physical device）

    初始化库之后，我们需要找到一张或者任意张（？？？）适配 的显卡。

  - 队列序列 

    vulkan中所有的操作都需要提交到队列中，队列的类型不同，处理的操作也是不同的，这里是列出哪些队列可以使用，为下面铺垫。

  - 逻辑设备

    - 描述我们需要使用的功能
    - 指定要创建的队列（上面已经查询到了）

- ### 介绍

  - 窗口表面

    需要利用GLFW创建一个表面。需要知道系统中的哪些设备支持它。因此，我们需要扩展isDeviceSuitable  确保设备可以展示surface。实际上是在找支持surface的队列系列。

    需要修改寻找队列和逻辑设备创建的代码（改成针对surface）。

  - 交换链

    vulkan没有提供默认缓冲区，需要手动构建一个交换链（缓冲区），在屏幕上可视化他们。本质是等待呈现的图像队列。

    - 找到可以用的扩展，但是必须进一步查细节（窗口表面的兼容性：基本功能（maxmin高度宽度），表面格式（像素，色彩空间），可用的演示效果
    - 启用这些扩展 + 进行合适的设置
    - 演示模式：向屏幕显示图像的实际条件（4种各有千秋）
    - 交换范围：分辨率类似

  - 图像视图

    在pipeline中使用VkImage,要创建一个对象

- ### 图像管道

  ​                                          <img src="C:\Users\77043\AppData\Roaming\Typora\typora-user-images\image-20250223191411405.png" alt="image-20250223191411405" style="zoom:67%;" />

  在将代码传递到管道之前，我们必须将其包装在 [`VkShaderModule`](https://www.khronos.org/registry/vulkan/specs/1.0/man/html/VkShaderModule.html) 对象，需要一个模块。流程大概是:

  ```
  读文件（字节码）----> 创建一个着色器模块 -----> 创建好分配信息 ------> 固定到管道 ----> 一些迷惑行为（光栅化，多重采样）
  ```

- ### 帧缓冲区

- ### 命令缓冲区

  
