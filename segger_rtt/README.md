segger_rtt
===

RTT（Real Time Transfer）是 SEGGER 公司开发的一种实时传输技术，可在不中断目标系统运行的情况下，通过调试接口（如 J-Link）实现主机与目标设备之间的高速数据传输，非常适合嵌入式系统的调试。

https://www.segger.com/products/debug-probes/j-link/technology/about-real-time-transfer  
https://wiki.segger.com/RTT

## 包含文件

  * `RTT/`
    * `SEGGER_RTT.c`               - RTT 的核心实现文件
    * `SEGGER_RTT.h`               - RTT 的核心头文件，包含主要 API 声明
    * `SEGGER_RTT_ASM_ARMv7M.S`    - 针对 ARMv7M 架构处理器（如 Cortex-M3/M4/M7）的汇编优化实现
    * `SEGGER_RTT_Printf.c`        - 提供SEGGER_RTT_printf()函数，支持通过 RTT 输出格式化字符串
  * `Syscalls/`
    * `SEGGER_RTT_Syscalls_*.c`    - 针对不同工具链的底层系统调用实现，用于将标准printf()重定向到 RTT
  * `Config/`
    * `SEGGER_RTT_Conf.h`          - RTT 的配置文件，可用于调整缓冲区大小、模式等参数

## 使用方法
将本项目作为子模块添加到您的项目中，或直接复制到项目目录
在您的主 CMakeLists.txt 中添加：
```cmake
    add_subdirectory(components/segger_rtt)
```
链接 RTT 库到您的目标：
```cmake
    target_link_libraries(${CMAKE_PROJECT_NAME} PRIVATE segger_rtt)
```