# 作業系統 OS

* [ccc: Linux 作業系統核心](http://ccckmit.wikidot.com/lk:main)

## OS 概念

* https://www.tutorialspoint.com/operating_system/index.htm
    * https://www.tutorialspoint.com/operating_system/os_properties.htm
    * https://www.tutorialspoint.com/operating_system/os_processes.htm
    * https://www.tutorialspoint.com/operating_system/os_process_scheduling_algorithms.htm
    * https://www.tutorialspoint.com/operating_system/os_multi_threading.htm
    * https://www.tutorialspoint.com/operating_system/os_virtual_memory.htm
    * https://www.tutorialspoint.com/operating_system/os_io_hardware.htm

## OS 實務

* [啟動程式 (BootLoader)](bootLoader)
* [線程 (Thread)](thread)
* [行程 (Process)](process)
* [行程通訊 (Inter Process Communciation)](ipc)
* [排程 (Scheduling)](scheduling)
* [記憶體管理 (Memory Management)](memoryManagement)
* [輸出入 (io)](io)
* [中斷 (interrupt)](interrupt)
* [工作切換 (Task Switch)](taskSwitch)

## 參考文獻

* https://www.facebook.com/groups/system.software2019/permalink/325874844797045/

> [Week5] 本週進度是 Linux 的 process/thread，不免會探討到 fork() 系統呼叫，需要留意的是，在 1969 年開發的 UNIX 第一版就提供 fork 系統呼叫，至今恰好滿 50 年，當初提出有其時空意義 (存在 Multics 的影子)，但 fork 在現代計算機架構上運作的類似 UNIX 作業系統 (如 Linux 和 FreeBSD)，實作有其彆扭之處，例如經典的 fork+exec 的「最佳化」(透過 lazy fork)，於是來自 Microsoft Research, Boston University, ETH Zurich 等單位的研究人員，回顧這 50 年間 fork 系統呼叫的發展和探討其侷限，建議人們改用 posix_spawn (這是 POSIX.1-2001 規範的一部分) 並徹底捨棄 fork 的使用。

