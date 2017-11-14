IP库
管理IP＝ array();
业务IP= array();
交换机= array();

服务器导入
$hostclient = array({
  '1' => array(
     'product' => array( //产品信息
       'product_name', 
       'default_business' => array('business_name', 'business_value'), 
       'price' => array('user_level', 'price'),
       'custom_config => array('business_name', 'business_value', price),
       'default_part' => array(
         'cup' =>,
         'mainboard'=>,
         'memory'=> array(),
         'harddisk'=> array(),
         'chassis' =>
       ),
     ),
     'server' => array( //服务器信息
       'cup' =>,
       'mainboard'=>,
       'memory'=>,
       'harddisk'=>,
       'chassis' =>,
       'ipm' => '管理Ip',
       'ipb' => array('业务IP1', '业务IP2'),
       'switch_P' = '交换机P'
       'switch_m' = ‘交换机M’,
       'size' => '占用几U'
     ),
     'room_info' = array(
        'room_name' => '机房名称'，
        'Area' => '地址'，
        'cabinet_number' => '机柜数'
        'cabinet' => array(
          'code' => '机柜编号'，
          'seat_number' => '机位数',
          'seat' => '所在机位如＃1'
        ),
      ),
     'client' => array(//客户信处
       'login_name' => '',
       'login_pwd' => '',
       'email' => '',
       'roles' => array(),
       'user_name' => '客户名称'
       'user_type' => '客户为型：个人还是企业'
     );
     'equipment_date' => '开始时间'
     'service_expired_date' => '到期时间'
     'description' => '备注'
     'trial' => '是否是试用'
  )
});
   
$user = array(
  '1' = array(
    'name' => '' ,
    'pwd' => '123456' ,
    'mail' => '',
    'status' = '', //0锁定 1启用
    'type' => ''   //client/employee
  )
);

$client = array(
  '1' = array(
    'uid' => '',
    'nick' => '',
    'clien_name' => '',
    'client_type' => '' ,  //个人/企业
    'corporate_name' => '',
    'qq' => '',
    'telephone' => '',
    
  )
);

$employee = array(
  '1' => array(
    'uid' => '',
    'employee_name' => '',
    'department' => '',
    'position' => '',
    'qq' => '',
    'telephone' => '',
    'address' => ''
  )
);
