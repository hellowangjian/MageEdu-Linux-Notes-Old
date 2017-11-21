## Linux 命令行使用技巧
<http://www.oschina.net/translate/most-useful-linux-command-line-tricks>
#### 将输出内容做一个清晰明了的表格
使用 `column` 命令：  

    column -columnate lists
        column option [file ...]

        option:
            -t：默认使用空格制表显示每一列。
            -s：指定 -t 选项使用的制表符。

Example：
```
    ~]# mount | column -t
    /dev/sda2                on  /                         type  ext3         (rw)
    proc                     on  /proc                     type  proc         (rw)
    sysfs                    on  /sys                      type  sysfs        (rw)
    devpts                   on  /dev/pts                  type  devpts       (rw,gid=5,mode=620)
    tmpfs                    on  /dev/shm                  type  tmpfs        (rw)
    /dev/sda1                on  /boot                     type  ext3         (rw)
    none                     on  /proc/sys/fs/binfmt_misc  type  binfmt_misc  (rw)
    /dev/mapper/myvg-mydata  on  /mydata                   type  ext4         (rw)

    指定使用冒号“：”制表显示：
    ~]# cat /etc/passwd | column -t -s :
    root       x  0    0    root                          /root                /bin/bash
    bin        x  1    1    bin                           /bin                 /sbin/nologin
    daemon     x  2    2    daemon                        /sbin                /sbin/nologin
    adm        x  3    4    adm                           /var/adm             /sbin/nologin
    lp         x  4    7    lp                            /var/spool/lpd       /sbin/nologin
    sync       x  5    0    sync                          /sbin                /bin/sync
    shutdown   x  6    0    shutdown                      /sbin                /sbin/shutdown
    halt       x  7    0    halt                          /sbin                /sbin/halt
    mail       x  8    12   mail                          /var/spool/mail      /sbin/nologin
    uucp       x  10   14   uucp                          /var/spool/uucp      /sbin/nologin
```

#### 重复执行一个命令，直到它运行成功
```
    ~]# while true
    > do
    > ping -c 1 baidu.com > /dev/null 2>&1 && break
    > done;

```

#### 按内存资源的使用量对进程进行排序
```
    ~]# ps aux | sort -rnk 4 | head
```

#### 按 CPU 资源的使用量对进程进行排序
```
    ~]# ps aux | sort -rnk 3 | head
```