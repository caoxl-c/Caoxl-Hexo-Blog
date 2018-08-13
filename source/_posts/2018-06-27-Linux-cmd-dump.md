---
title: Linux 命令 「dump」
date: 2018-06-27 10:24:43
categories: Linux cmd
tags: [Linux]
---

> `dump`命令用于备份`ext2`或者`ext3`文件系统。可将目录或整个文件系统备份至指定的设备，或备份成一个大文件。

<!-- more -->

# 语法选项

- `-0123456789`:  备份的层级
- `-b<区块大小>`:   指定区块的大小,单位为`KB`
- `-B<区块数目>`:   指定备份卷册的区块数目
- `-c`:     修改备份磁带预设的密度和容量
- `-d<密度>`:     设置磁带的密度,单位为`BPI`
- `-f<设备名称>`:  指定备份设备
- `-h<层级>`:     当备份层级等于或大于指定的层级时,将不备份用户表示为`nodump`的文件
- `-n`:     当备份工作需要管理员介入时,向所有`operator`群组的使用者发出通知
- `-s<磁带长度>`:   备份磁带的长度,单位为英尺
- `-T<日期>`:     指定备份的时间和日期
- `-u`:     备份完毕后,在`/etc/dumpdates`中记录备份的文件系统,层级,日期与时间等
- `-w`:     与`-W`类似, 单仅需要备份的文件
- `-W`:     显示需要备份的文件及其最后一次备份的层级,时间,日期

# 参数

- 备份源:  指定要备份的文件、目录或者文件系统

# 实例

将`/home`目录所有内容备份到`/tmp/homeback.bak`文件中，备份层级为`0`并在`/etc/dumpdates`中记录相关信息：

```
    dump -0u -f /tmp/homeback.bak /home
```

将`/home`目录所有内容备份到`/tmp/homeback.bak`文件中，
备份层级为`1`（只备份上次使用层次0备份后发生过改变的数据）并在`/etc/dumpdates`中记录相关信息：

```
    dump -1u -f /tmp/homeback.bak /home
```

> 通过`dump`命令的备份层级，可实现`完整+增量备份`、`完整+差异备份`，在配合`crontab`可以实现`无人值守备份`。