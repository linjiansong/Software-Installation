# 安装Windows提示无法在驱动器0分区上安装windows解决方法

## 原因分析：
```
win8/win10系统均添加快速启动功能，预装的win8/win10电脑默认都是UEFI引导和GPT硬盘；
传统的引导方式为Legacy引导和MBR硬盘，UEFI必须跟GPT对应，同理Legacy必须跟MBR对应。
如果BIOS开启UEFI，而硬盘分区表格式为MBR则无法安装；BIOS关闭UEFI而硬盘分区表格式为GPT也是无法安装Windows。
```
## 解决方式：
```
1、在当前安装界面按住Shift+F10调出命令提示符窗口；
2、输入diskpart，按回车执行；
3、进入DISKPART命令模式，输入list disk回车，列出当前磁盘信息；
4、要转换磁盘0格式，则输入select disk 0回车，输入clean，删除磁盘分区；
5、输入convert mbr，回车，将磁盘转换为MBR，输入convert gpt则转为GPT；
6、最后输入exit回车退出命令提示符，返回安装界面继续安装系统。
------------
进入pe系统通过DiskGenius软件查看硬盘分区表类型是gpt还是mbr格式
```
