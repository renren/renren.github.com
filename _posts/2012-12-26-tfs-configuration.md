---
layout: post
title: "TFS配置文件"
description: ""
category: TFS 
tags: []
author: 'Wang Ning'
contributors: ['Wang Ning']
---
{% include JB/setup %}

    [public]
<br/>


日志级别，**可选设置**，默认为**debug** 

线上建议设置为INFO，调试时设为DEBUG，有效值是"ERROR","WARN","INFO","DEBUG"，不区分大小写

    log_level = INFO [ ERROR|WARN|INFO|DEBUG ]
<br/>

日志文件的大小，单位Byte，**可选设置**，默认为**1GiB**，超过该大小后日志将被转储

    log_size = 1073741824
<br/>

保留日志文件的个数，**可选设置**，默认为**16**

以nameserver为例，所有日志文件保存在work_dir/logs目录，正在写的文件是nameserver.log。当nameserver.log大小超过log_size时，nameserver.log改名为nameserver.log.%Y%m%d%H%M%S，其中YmdHMS分别代表年月日时分秒。如果nameserver进程启动后写入的log文件数目超过了log_num，则删除最早生成的那个log文件，最后重新打开nameserver.log。需要注意的是，work_dir/logs目录下的日志文件数量可能远大于log_num，log_num控制的是每次nameserver进程生存期内最多产生的log文件数量

    log_num = 16
<br/>

工作线程数量，**可选设置**，默认为**8**

TFS底层网络编程框架采用tbnet库以简化消息的处理。tbnet接收和处理包的过程符合生产者-消费者模型。tbnet网络IO线程收到数据后还原为TFS Message，然后放入一全局工作队列中，有多个消费者线程从全局队列取得Message，执行相应的消息处理函数。thread_count指定消费者线程数量

    thread_count = 4
<br/>

工作队列大小，**可选设置**，默认是**10240**

指定工作队列中最多能存放的TFS Message数目，最小为10240，最大为40960

    task_max_queue_size = 10240
<br/>

工作目录，**可选设置**，默认为**/tmp**

该目录下的logs目录存放日志文件，根据服务的不同，工作目录下还会存储一些持久化数据。因为/tmp下的数据易失，强烈建议改掉默认设置

    work_dir = /data/tfs
<br/>

网络设备，**必须设置**

    dev_name = bond0
<br/>


对外提供服务的IP地址，**必须设置**

服务配置HA时设置为VIP，没配置HA可以设为master的IP

    ip_addr = 192.168.0.1
<br/>

监听端口, **必须设置**，从1024~65535中选取

    port = 8108

