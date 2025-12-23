# Linux

## 1 概论

### 1.1 如何下载 **wsl**

### 1.2 各硬件设备在 Linux 中的文件名

在 Linux 中，每个设备都被当成一个文件来对待， 举例来说，SATA 接口的硬盘文件名称是 `/dev/sd[a-d]`，即 `/dev/sda`、`/dev/sdb` 等

下面列出几个常见的设备与在 linux 中的文件名

| 设备               | 在 linux 中的文件名                                                 |
|:---------------- |:------------------------------------------------------------- |
| SCS/SATA/USB 硬盘机 | `/dev/sd[a-p]`                                                |
| USB 闪存盘          | `/dev/sd[a-p]` (同上)                                           |
| Virtl/0界面        | `/dev/vd[a-p]` 用于虚拟机内                                         |
| 软盘机              | `/dev/fd/[0-7]`                                               |
| 打印机              | `/dev/lp[0-2]` 25 针打印机、`/dev/usb/lp[0-15]` USB 打印机            |
| 鼠标               | `/dev/input/mouse` 通用、`/dev/psaux` PS/2 界面、`/dev/mouse` 当前鼠标  |
| CDROM/DVDR0M     | `/dev/scd[0-1]` 通用、`/dev/sr[0-1]` 通用，Cent0s常见、`/dev/cdrom` 当前 |
| 磁带机              | 太老不记录                                                         |
| IDE 硬盘机          | `/dev/hd[a-d]` 老式系统才有                                         |

要注意的是使用云端机时，你得到的是虚拟机，为了加速，虚拟机内的磁盘使用仿真机产生，一般被命名为 `/dev/vd[a-p]`

## 2 基础指令和常用热键

### 2.1 指令的组成

```bash
command [-options] parameter1 parameter2
```

- command：指令名，也可以替换为 可执行文件名（如批次脚本script）
- \[-options\]：可选配置参数（实际不包含\[\]）
  - `-`一个短横线是选项的简写
  - `--`两个短横线是选项的全写
- 指令、选项、参数等中间以空格来区分，不论空几格都视为一格
- 按下 **enter** 键后启动命令
- 使用反斜杠 **\\** 使 **enter** 后指令持续到下一行
- 使用 `quit` 主动退出执行的命令

### 2.2 基础指令

#### date

```bash
[mrcode@study ~]$ date
Fri Oct  4 23:41:16 CST 2019
# 格式化输出
[mrcode@study ~]$ date +%Y/%m/%d
2019/10/04
[mrcode@study ~]$ date +%H:%M
23:41
```

#### cal

需安装`badmainutils`：

```bash
sudo apt update  # 可选：更新软件源索引，避免安装失败
sudo apt install -y bsdmainutils
```

```bash
# 显示当前月
[mrcode@study ~]$ cal
    October 2019    
Su Mo Tu We Th Fr Sa
       1  2  3  4  5
 6  7  8  9 10 11 12
13 14 15 16 17 18 19
20 21 22 23 24 25 26

# 显示整年，这里只贴出部分
[mrcode@study ~]$ cal 2019
                               2019                               

       January               February                 March       
Su Mo Tu We Th Fr Sa   Su Mo Tu We Th Fr Sa   Su Mo Tu We Th Fr Sa
       1  2  3  4  5                   1  2                   1  2
 6  7  8  9 10 11 12    3  4  5  6  7  8  9    3  4  5  6  7  8  9
13 14 15 16 17 18 19   10 11 12 13 14 15 16   10 11 12 13 14 15 16
20 21 22 23 24 25 26   17 18 19 20 21 22 23   17 18 19 20 21 22 23
27 28 29 30 31         24 25 26 27 28         24 25 26 27 28 29 30
                                              31
        April                   May                   June        
Su Mo Tu We Th Fr Sa   Su Mo Tu We Th Fr Sa   Su Mo Tu We Th Fr Sa
    1  2  3  4  5  6             1  2  3  4                      1
 7  8  9 10 11 12 13    5  6  7  8  9 10 11    2  3  4  5  6  7  8
14 15 16 17 18 19 20   12 13 14 15 16 17 18    9 10 11 12 13 14 15
21 22 23 24 25 26 27   19 20 21 22 23 24 25   16 17 18 19 20 21 22
28 29 30               26 27 28 29 30 31      23 24 25 26 27 28 29

```

```bash
[mrcode@study ~]$ cal 10 2015
    October 2015    
Su Mo Tu We Th Fr Sa
             1  2  3
 4  5  6  7  8  9 10
11 12 13 14 15 16 17
18 19 20 21 22 23 24
25 26 27 28 29 30 31

```

#### bc计算器

```bash
[mrcode@study ~]$ bc
10*52
520
10^2 #幂运算使用^
100
10/100 
0
# 在 bc 环境中，使用 scale = 数值
# 后面数值表示你需要几位小数
scale=3
10/100
.100
```

### 2.3 求助

#### --help

前面已经讲到指令的组成为 `command [-options] parameter1 parameter2`  ，在 command 后使用 **-h** 或 **--help** 查询指令的帮助文档 。

--help 用在协助查询已用过的指令的选项和参数。

```bash
date --help
Usage: date [OPTION]... [+FORMAT]
  or:  date [-u|--utc|--universal] [MMDDhhmm[[CC]YY][.ss]]
Display date and time in the given FORMAT.
With -s, or with [MMDDhhmm[[CC]YY][.ss]], set the date and time.

Mandatory arguments to long options are mandatory for short options too.
  -d, --date=STRING          display time described by STRING, not 'now'
      --debug                annotate the parsed date,
                              and warn about questionable usage to stderr
  -f, --file=DATEFILE        like --date; once for each line of DATEFILE
```

#### man page

**man** 指manual操作说明，按照`man command`即可获得更为详细的指令说明 **man page**。

```bash
[mrcode@study ~]$ man date
# 注意括号中的数字
DATE(1)                             User Commands                             DATE(1)

NAME   # 这个指令的完整名称，如下所示为 date 且说明简单用途为 设置与显示日期/时间
       date - print or set the system date and time

SYNOPSIS # 简介：这个指令的基本语法如下
       date [OPTION]... [+FORMAT]   # 单纯显示用法
       date [-u|--utc|--universal] [MMDDhhmm[[CC]YY][.ss]]  # 可以设置系统时间的方法

DESCRIPTION # 详细描述，刚刚谈到的选项与参数的用法
ENVIRONMENT # 与这个指令相关的环境参数的说明
EXAMPLES # 一些示例用法
DATE STRING  # 这里就解释了上面那个 STRING 是什么
AUTHOR # 这个指令的作者
COPYRIGHT # 受到著作权法的保护，用的就是 GPL
SEE ALSO # 这个重要，你还可以从哪里查到与 date 相关的说明文件的意思
```

最开始的标签 **DATE(1)** 中的数字具有含义：

| 代号  | 含义                         |
| --- | -------------------------- |
| 1   | 用户在 shell 环境中可以操作的指令或可执行文件 |
| 5   | 配置文件或则是某些文件的格式             |
| 8   | 系统管理员可用的管理指令               |

在 **man page** 中可以使用一些快捷键，如“空格-向下翻页”“PGUP”“PGDN”“home-第一页”“end-末页”“q-退出man page”。

使用 `man -f command` 可以 **精确** 匹配命令名，使用 `man -k part_of_command` 可以 **模糊**匹配命令名。

```bash
man -f man
man (1)              - an interface to the system reference manuals
```

输出的字段分别为 命令名（man），手册节号（(1)，之前有讲其意义），功能描述。

#### info page

info 和 man 的用途相近，输出较好，使用 ``info command`` 查询命令的说明。

```bash
info info
Next: Stand-alone Info,  Up: (dir)

Stand-alone GNU Info
********************

This documentation describes the stand-alone Info reader which you can
use to read Info documentation.

   If you are new to the Info reader, then you can get started by typing
‘H’ for a list of basic key bindings.  You can read through the rest of
this manual by typing <SPC> and <DEL> (or <Space> and <Backspace>) to
move forwards and backwards in it.

* Menu:

* Stand-alone Info::           What is Info?
* Node Commands::              Commands for selecting a new node.


 -- The Detailed Node Listing --

Selecting Cross-references

* Parts of an Xref::           What a cross-reference is made of.
* Selecting Xrefs::            Commands for selecting menu or note items.
```

含 **\*** 且带下划线的部分，可通过“PGUP”和“PGDN”移动到其上再按回车，进行超链接跳转。

### 2.4 常用热键

#### tab

**tab** 具有 **命令补全、文件补齐、选项/参数补齐** 的功能。

```bash
mkdir    #输入mkd后按下tab自动补齐为mkdir

git        #此处按1下或连按2下tab
git                 git-shell           git-upload-pack     
git-receive-pack    git-upload-archive
```

按一下tab优先尝试补全命令或文件名，按两下tab优先列出所有匹配项。但是在我的电脑中， **只能进行按一次tab** ，进行了交互优化。

#### ctrl + c

使用 **ctrl+c** 中断命令，注意是中断命令的输入而非执行，比如在输入命令时发现前面输错，需要重新输入，使用ctrl+c进行中断。

```bash
j^C        #^C终止了命令的输入
        #新起输入行
```

#### ctrl + d

使用 **ctrl+d** 发送正常结束符。

### 2.5 正确关机

#### shutdown

该命令会通知系统内的各个程序（processes）、服务等进行关闭，shutdown 可以达成以下工作：

- 可以自由选择关机模式：关机或重启
- 可以设定关机时间：立刻、未来的一个时间
- 可以自定义关机信息：在关机前，将设置的信息广播给在线的 user
- 可以仅发出警告信息：有时候可能需要测试、或则明确告知使用者的场景下，就可以使用该功能，但是可以不关机

语法如下：

```bash
/sbin/shutdown [-krhc] [时间 [警告信息]]
```

- k：不要真的关机，只发送警告信息
- r：在将系统的服务停掉之后就重新启动（常用)
- h：将系统的服务停掉之后，立即关机（常用）
- c：取消已经在进行的 shutdown 指令内容
- 时间：指定系统关机的时间，若没有时间，则默认 1 分钟后自动进行

#### reboot

重启

#### poweroff

关机
