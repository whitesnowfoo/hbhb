## Myslq 常用命令


```mysql

-- 分析mysql的实例的情况
show processlist;

-- 查看表是否太大 
show table status like 't_xx' ;

-- 查看引擎状态
show engine innodb status ;

-- 查找当前等待事务：
select * from  performance_schema .events_waits_current;

-- 查找事务
select * from information_schema.innodb_trx;

-- 建库
CREATE DATABASE `esr` DEFAULT CHARACTER SET utf8 COLLATE utf8_general_ci; 

-- 建所有权限用户
grant all privileges on *.* to root@'%' identified by 'root';
grant all privileges on *.* to esr@'192.168.%' identified by '123';

-- 建查询权限用户
GRANT SELECT ON `nutch`.`t_wdt_order_goods` TO 'phpw'@'%';

-- 刷新权限
flush privileges; 

-- 带条件导出SQL
-- mysqldump -u root -p nutch tbname -w="id>123456789" > xxxx.sql;

-- 数据字典
SELECT TABLE_SCHEMA,TABLE_NAME,COLUMN_NAME,COLUMN_TYPE,COLUMN_KEY,COLUMN_COMMENT 
FROM information_schema.columns WHERE TABLE_SCHEMA='nutch' 


-- 创建function
delimiter ;;

DROP FUNCTION IF EXISTS fun_rand_key ;;

CREATE FUNCTION fun_rand_key(iparam int) RETURNs int
BEGIN
   declare i_return int;
   set i_return =iparam + floor(rand()*100);
   return i_return;
END;
 ;;

delimiter ;
```