Zatree简介
==================================
当zabbix走进千家万户的时候，我们也许需要做点什么。

zatree是监控软件zabbix的一个插件，主要功能是提供host group的树形展示和在item里指定关键字查询及数据排序。

测试过2.0.6和2.0.7版本，理论上2.0.X的都应该支持，如果不支持我也没办法，自己动手改改吧。

Zatree安装
==================================
1：下载文件

git clone https://github.com/spide4k/zatree.git zatree

2：复制相关文件

假如zabbix web目录位置在/var/www/zabbix,定义zabbix目录

ZABBIX_PATH=/var/www/zabbix

复制相关文件和目录

cp -rf zatree $ZABBIX_PATH/

cd $ZABBIX_PATH/zatree/addfile

cp class.cchart_zabbix.php class.cgraphdraw_zabbix.php class.cimagetexttable_zabbix.php $ZABBIX_PATH/include/classes/

cp zabbix.php zabbix_chart.php $ZABBIX_PATH/

cp CItemValue.php $ZABBIX_PATH/api/classes/

3：支持web interface,修改配置文件

vi $ZABBIX_PATH/zatree/zabbix_config.php

'user'=>'xxx', //你的用户名

'passowrd'=>'xxx', //你的密码

4：导航增加Zatree入口,修改menu.inc.php，main.js

vi $ZABBIX_PATH/include/menu.inc.php

添加285行到294行内容

    285         'zatree'=>array(
    286                 'label' => _('zatree'),
    287                 'user_type'                             => USER_TYPE_ZABBIX_USER,
    288                 'default_page_id'       => 0,
    289                 'force_disable_all_nodes' => true,
    290                 'pages' =>array(
    291                         array('url' => 'zabbix.php','label' => _('Zatree'),)
    292                         )
    293         
    294         ),      
    295         
    296         'login' => array(                               
    297                 'label'                                 => _('Login'),
    298                 'user_type'                             => 0,
    299                 'default_page_id'               => 0,

vi $ZABBIX_PATH/js/main.js

替换106行

menus:                  {'empty': 0, 'view': 0, 'cm': 0, 'reports': 0, 'config': 0, 'admin': 0, 'zatree':0},

6：增加封装的api类


vi $ZABBIX_PATH/include/classes/api/API.php

在74行下添加75行'itemvalue'=>'CItemValue',

     74                 'usermedia' => 'CUserMedia',
     75                 'itemvalue'=>'CItemValue',
     76                 'webcheck' => 'CWebCheck'
     77         ); 

7：登陆zabbix，在导航里可以看到一个Zatree的菜单，使用方法是傻瓜的


技术支持
==================================
http://weibo.com/spider4k

http://weibo.com/chinahanna

http://weibo.com/678236656

祝玩的愉快

