牵引系统模块设计
目的:
  1.将原来牵引系统的功能移到drupal中来。
  
说明:
  要移去的功能点：
    1.牵引系统配置   
    2.流量牵引策略
    3.临时牵引策略
    4.流量清洗牵引
    5.滤后牵引状态
    6.ip封停
    7.牵引历史
    8.滤后牵引历史
    9.IP封停历史
    10.临时牵引历史
    11.攻击图表
    12.独立IP检查
    13.后台首页

设计思路:
  表结构不变，请求改变。

一、配置变量

二、请求设计
  admin/qy: 牵引系统菜单列表
  admin/qy/configure: 牵引系统配置
  admin/qy/policy: 流量牵引策略
  admin/qy/policy/add: 增加流量牵引策略
  admin/qy/policy/{policy_id}/edit: 修改流量牵引策略
  admin/qy/policy_tmp: 临时牵引策略
  admin/qy/policy_tmp/add: 增加临时牵引策略
  admin/qy/policy_tmp/{policy_id}/edit: 修改临时牵引策略
  admin/qy/policy_tmp/{policy_id}/status/{status}: 开启关闭
  admin/qy/policy/{policy_id}/delete: 删除流量牵引策略
  admin/qy/traction: 流量清洗牵引
  admin/qy/traction/add: 增加流量清洗牵引
  admin/qy/ajax/list: ajax获取列表数据
  admin/qy/traction_filter: 滤后牵引状态
  admin/qy/ip_stop: ip封停
  admin/qy/ip_stop/add：增加IP封停
  admin/qy/traction/{traction_id}/remove: 解除牵引
  admin/qy/traction/{traction_id}/time: 修改解牵引时间
  admin/qy/traction/remove/alarm: 解除全部Alarm
  admin/qy/attack: 攻击图表
  admin/qy/ip_check: 独立IP检查
  admin/qy/index: 后台首页
  admin/qy/logs/traction: 牵引过的ip日志
  admin/qy/logs/traction_filter: 滤后牵引历史
  admin/qy/logs/ip_stop: IP封停历史
  admin/qy/logs/traction_tmp: 临时牵引历史

  //------防火墙---------
  admin/qy/open/151

三、权限设计

四、实体设计

五、数据库设计

 sys(牵引系统配置-全局系统设置)
    id:         int     主键
    bps：       varchar BPS流量
    pps：       varchar PPS流量
    time：      int     牵引时间
    max_index:  int(50)     最大的索引值
    last_index: int     最后一条index
    ip1:        varchar
    ip2:        varchar
    o_bps:      varchar
    o_pps:      varchar
    o_time:     int
    start:      int 
    pass:       int 
    all_kill:   int(10)     全局多少秒
    now_kill:   int     目前的时间
    alarm_bps:  varchar(6500) 触发BPS值

  sys_alarm(牵引系统配置-设置Alarm值或临时alarm值设置)
    id:                    int      主键
    user:                  varchar  操作员
    alarm_bps:             varchar(65000)  电信BPS
    alarm_bps_one:         varchar(9000)  电信单墙BPS
    max_index:             int(50)      最大rule索引值
    max_qy_count:          int(25)      最大的牵引数
    net_com_alarm_bps:     varchar(10)  联通MAX bps
    net_com_alarm_bps_one: varchar(200)  联通单墙 bps
    net_com_alarm_time:    int(5)      联通TIME
    hw_bps_one:            varchar  海外联通单墙 bps
    hw_alarm_bps:          varchar  海外联通MAX bps
    hw_alarm_time:         int      海外联通TIME
    ls_alarm_ctrl：        int      是否开启alarm值(1开启；2关闭)
    ls_alarm_count：       int(5)      alarm次数阀值-次数
    ls_alarm_count_time:   int(1)      alarm次数阀值-分钟
    ls_alarm_bps：         varchar(65000)  临时alarm值
    ls_alarm_time：        int(10)      临时alarm保持时间
    last_index:            int      最后一条index
    ls_alarm_start:        int      第一次的时间
    ls_alarm_start_fuck:   int 
    ls_now_count:          int 

  t_policy(策略表)
    id:                 int      主键
    ip：                varchar  策略针对的IP
    net_type:           int(1)      网络类型(1电信 2网通-该操作对应牵引命)
    ms:                 int(1)      牵引模式(1.独享、2.共享-只认正常流量牵引条件，不认超大流量牵引条件)
    note:               varchar  备注
    bps:                varchar  流量阀值－正常流量牵引条件
    pps:                varchar  包阀值－正常流量牵引条件
    time:               float    牵引时间－正常流量牵引条件
    cbps:               varchar  流量阀值－超大流量牵引条件
    cpps:               varchar  包阀值－超大流量牵引条件
    ctime:              int      牵引时间－超大流量牵引条件
    gbps:               varcahr  保障流量阀值－共享保障值
    gpps:               varchar  保障包阀值－共享保障值
    gtime:              int      保障牵引时间－共享保障值
    ddh：               varchar  订单号
    khh：               varchar  客户号
    starts：            varchar  开通日期
    end：               varchar  到期日期
    kills:              int(1)      临时牵引和防护测试里设置的结束时间
    xx:                 int(1)      牵引种类(0为流量牵引；1为订单牵引,3临时，4防护 5客户 6虚拟)
    opter:              varchar(sys)  操作员登录名
    depart：            varchar(0)  部门
    time_b：            int      随机时间-big
    zt：                int      暂停
    ycid：              int      远程id
    fd_jg_b：           int      发动时间间隔-big
    fd_jg：             int      发动时间间隔
    min_bps：           varchar  浮动范围:最小值
    max_bps：           varchar  浮动范围:最大值
    whosyourdaddy：     varchar 
    v_time：            int      虚拟运行的时间
    yd_start：          int      预定-开始时间
    yd_end：            int(24)   预定-结束时间
    cl_start:           int      开始时间
    ips：               text
    mg_ip_time：        int      一群IP中变换时间
    pre_ip_need_tine：  int       当前群IP的次数
    cl_time：           int      0代表自己设置 1：按原策略
    use_time:           int      使用策略的时间
    last_do_time:       int      上次运行时间
    remote_version:     int     远程版本
    why_no:             int 

  t_qy(牵引表)
    id:                 int     主键
    ip:                 varchar 牵引的IP
    net_type：          tinyint(1) 牵引线路(1全局、2联通、3海外)
    pps:                varchar 牵引时的pps流量
    bps:                varchar 牵引时的bps流量
    start：             int     牵引的时间
    time：              varchar 牵引多少时间后解封(0 代表永久)
    type:               varchar 牵引类型（bps：超bps流量而牵引的IP；pps: 超pps流量而牵引的ip；cleaning：伪造流量使其牵引的IP；手动增加的；等）
    note：              varchar 备注
    opter：             varchar(sys) 操作员（如果是sys是设备自动牵引的）
    depart：            varchar 部门
    gjft：              int(1)     1牵引; 2封停; 3虚拟攻击
    uid：               int     客户Id
    cgf:                int(1)     牵引成功否
    counts:             int(1)     牵引次数
    cgf_starttimer：    varcahr(0) 执行命令的开始时间
    cgf_stoptimer：     varchar(0) 执行命令的结束时间
    cgf_startmicrotime：float   执行命令的开始时间(微秒部分)
    cgf_stopmicrotime： float   执行命令的结果时间(微秒部分)
    this_index：        int 
    bps_y：             varchar 
    pps_y：             varchar 

  t_logs(日志)
    id:      int     主键
    ip:      varchar 牵引IP
    bps:     varchar bps流量
    pps：    varchar pps流量
    start：  int     开始时间
    end：    int     结束时间
    type：   varcahr 牵引类型
    note：   varchar 备注
    opter：  varchar(sys) 操作员
    depart： varchar 部门
    sy:      int     note == 'A'?'0' : $row['start'] + $row['time'] * 60 - time()
    counts:  int(1)     牵引次数
    wm:      varchar 命令执行时间
    uid：    varchar 客户
    log:     int     1是牵引；2是封停
    xx:      int 
 
六、APIs设计

