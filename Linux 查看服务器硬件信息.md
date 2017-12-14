## Linux 查看服务器硬件信息

>https://yq.aliyun.com/articles/38704?spm=5176.100239.blogcont38702.33.ArX8PN  
>http://www.51testing.com/html/38/225738-236367.html

#### 1、 查看 CPU 信息

- 查看 CPU 型号信息

        # cat /proc/cpuinfo | grep "model name"
        model name  : Intel(R) Xeon(R) CPU           X5570  @ 2.93GHz
        model name  : Intel(R) Xeon(R) CPU           X5570  @ 2.93GHz
        model name  : Intel(R) Xeon(R) CPU           X5570  @ 2.93GHz
        model name  : Intel(R) Xeon(R) CPU           X5570  @ 2.93GHz
        model name  : Intel(R) Xeon(R) CPU           X5570  @ 2.93GHz
        model name  : Intel(R) Xeon(R) CPU           X5570  @ 2.93GHz
        model name  : Intel(R) Xeon(R) CPU           X5570  @ 2.93GHz
        model name  : Intel(R) Xeon(R) CPU           X5570  @ 2.93GHz
        model name  : Intel(R) Xeon(R) CPU           X5570  @ 2.93GHz
        model name  : Intel(R) Xeon(R) CPU           X5570  @ 2.93GHz
        model name  : Intel(R) Xeon(R) CPU           X5570  @ 2.93GHz
        model name  : Intel(R) Xeon(R) CPU           X5570  @ 2.93GHz
        model name  : Intel(R) Xeon(R) CPU           X5570  @ 2.93GHz
        model name  : Intel(R) Xeon(R) CPU           X5570  @ 2.93GHz
        model name  : Intel(R) Xeon(R) CPU           X5570  @ 2.93GHz
        model name  : Intel(R) Xeon(R) CPU           X5570  @ 2.93GHz

    说明：CPU 型号是至强 X5570，主频 2.93GHz。

- 查看逻辑 CPU 个数

        # cat /proc/cpuinfo | grep "processor" | wc -l
        16

- 查看物理 CPU 个数

        # cat /proc/cpuinfo | grep "physical id" | sort | uniq | wc -l
        2

- 每个物理 CPU 的 Core 个数

        # cat /proc/cpuinfo | grep "cpu cores" | uniq | awk -F: '{print $2}'
        4

- 每个物理CPU中逻辑CPU(可能是core, threads或both)的个数

        # cat /proc/cpuinfo | grep "siblings" | uniq 
        siblings    : 8

>/proc/cpuinfo 文件包含系统上每个处理器的数据段落。/proc/cpuinfo 描述中有 6 个条目适用于多内核和超线程（HT）技术检查：processor, vendor id, physical id, siblings, core id 和 cpu cores。  
processor 条目包括这一逻辑处理器的唯一标识符。  
physical id 条目包括每个物理封装的唯一标识符。  
core id 条目保存每个内核的唯一标识符。  
siblings 条目列出了位于相同物理封装中的逻辑处理器的数量。  
cpu cores 条目包含位于相同物理封装中的内核数量。  
如果处理器为英特尔处理器，则 vendor id 条目中的字符串是 GenuineIntel。  

>1.拥有相同 physical id 的所有逻辑处理器共享同一个物理插座。每个 physical id 代表一个唯一的物理封装。  
2.Siblings 表示位于这一物理封装上的逻辑处理器的数量。它们可能支持也可能不支持超线程（HT）技术。  
3.每个 core id 均代表一个唯一的处理器内核。所有带有相同 core id 的逻辑处理器均位于同一个处理器内核上。  
4.如果有一个以上逻辑处理器拥有相同的 core id 和 physical id，则说明系统支持超线程（HT）技术。  
5.如果有两个或两个以上的逻辑处理器拥有相同的 physical id，但是 core id 不同，则说明这是一个多内核处理器。cpu cores 条目也可以表示是否支持多内核。  

>判断CPU是否64位，检查cpuinfo中的flags区段，看是否有lm标识。  
Are the processors 64-bit?     
A 64-bit processor will have lm ("long mode") in the flags section of cpuinfo. A 32-bit processor will not.

#### 2、查看硬盘大小

    # fdisk -l | grep "sd[a-z]"
    Disk /dev/sda: 1348.5 GB, 1348485513216 bytes

####  3、查看内存信息 

    # dmidecode -t memory | head -n 32
    # dmidecode 2.12
    SMBIOS 2.6 present.

    Handle 0x1000, DMI type 16, 15 bytes
    Physical Memory Array
        Location: System Board Or Motherboard
        Use: System Memory
        Error Correction Type: Multi-bit ECC
        Maximum Capacity: 192 GB
        Error Information Handle: Not Provided
        Number Of Devices: 18

    Handle 0x1100, DMI type 17, 28 bytes
    Memory Device
        Array Handle: 0x1000
        Error Information Handle: Not Provided
        Total Width: 72 bits
        Data Width: 64 bits
        Size: 4096 MB
        Form Factor: DIMM
        Set: 1
        Locator: DIMM_A1 
        Bank Locator: Not Specified
        Type: DDR3
        Type Detail: Synchronous Registered (Buffered)
        Speed: 1333 MHz
        Manufacturer: 002C04B3802C
        Serial Number: D862FE12
        Asset Tag: 08094703
        Part Number: 36JSZF51272PZ1G4F1
        Rank: 2

#### 4、查看主板信息

    # dmidecode -q | more
    BIOS Information
        Vendor: Dell Inc.
        Version: 1.2.6
        Release Date: 07/17/2009
        Address: 0xF0000
        Runtime Size: 64 kB
        ROM Size: 4096 kB
        Characteristics:
            ISA is supported
            PCI is supported
            PNP is supported
            BIOS is upgradeable
            BIOS shadowing is allowed
            Boot from CD is supported
            Selectable boot is supported
            EDD is supported
            Japanese floppy for Toshiba 1.2 MB is supported (int 13h)
            5.25"/360 kB floppy services are supported (int 13h)
            5.25"/1.2 MB floppy services are supported (int 13h)
            3.5"/720 kB floppy services are supported (int 13h)
            8042 keyboard services are supported (int 9h)
            Serial services are supported (int 14h)
            CGA/mono video services are supported (int 10h)
            ACPI is supported
            USB legacy is supported
            BIOS boot specification is supported
            Function key-initiated network boot is supported
            Targeted content distribution is supported
        BIOS Revision: 1.2

    System Information
        Manufacturer: Dell Inc.
        Product Name: PowerEdge R710   //服务器型号
        Version: Not Specified
        Serial Number: 3Z69S2X
        UUID: 4C4C4544-005A-3610-8039-B3C04F533258
        Wake-up Type: Power Switch
        SKU Number: Not Specified
        Family: Not Specified

    Base Board Information
        Manufacturer: Dell Inc. 
        Product Name: 0VWN1R  //主板型号
        Version: A02
        Serial Number: ..CN137409BN02KE.  //序列号
        Asset Tag: Not Specified

    Chassis Information
        Manufacturer: Dell Inc.
        Type: Rack Mount Chassis
        Lock: Present
        Version: Not Specified
        .
        .
        .