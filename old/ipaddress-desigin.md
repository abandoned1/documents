*ipaddress-design.md* IPaddress(IP地址管理)[管理IP和业务IP]

说明:
1. 对IP地址管理，包括列表，编辑，IP地址分配

问题:
1. 需求问题:
  a) IP信息(管理｜业务)列表(IP，管理状态类型，业务类型，IP状态，所属机房，所属机柜，交换机，端口，默认配置，备注信息)
  b) 管理IP地址添加，业务IP地址添加
  c) 专用业务IP编辑，业务IP地址段编辑
  d) IP地址管理删除
  
一、 系统变量 ~

二、 请求设计 ~ 

三、 权限设计 ~

四、 对象设计 ~

五、 数据库设计 ~
ips(IP管理)
iid: IPID(主键) 
title: IP varchar(32)
mtype: 管理类型(管理IP或业务IP-从术语中获取类型ID) int 
btype: 业务类型(公用，托管或特殊-从术语中获取业务类型ID) int
status: IP状态(公用IP，保留IP或其他-从术语中获取状态ID) int
rid: 所属机房(机房ID-从术语中获取机房ID) int
cid：所属机柜(机柜ID-外键) int
switch: 交换机 varchar(255)
port: 端口 int
pid: 默认配置 (外键， 服务器产品ID) int
description: IP备注信息
六、 APIs设计 ~