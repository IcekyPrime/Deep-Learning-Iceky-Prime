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
