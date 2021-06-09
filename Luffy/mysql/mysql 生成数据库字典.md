## mysql生成数据字典

首先把所有表名放进一个文件里。
```
mysql -uroot -proot databasename -e 'show tables' > ./tables.txt

```

也可以直接把要生成的表名写进tables.txt里，一个表名一行。

然后运行下面脚本

```

#! /bin/bash

TABLES=`cat /home/data/tables.txt`
DIR=/home/data/tmp/
if [ ! -d $DIR  ];then
        mkdir $DIR
fi
cd $DIR


for tab in $TABLES;do

        SQL="SELECT COLUMN_NAME as '字段',COLUMN_TYPE as '类型',IS_NULLABLE as '空',IFNULL(COLUMN_DEFAULT,'') as '默认',IF(COLUMN_COMMENT='','-',COLUMN_COMMENT) as '注释'FROM information_schema.columns WHERE TABLE_SCHEMA='nutch' and table_name='${tab}'";
        #echo $SQL;
        mysql -uroot -p password -t -e "${SQL}"  > ./${tab}.txt
        sed -i "s/+/|/g" ./${tab}.txt
        sed -i '$d' ./${tab}.txt
        sed -i "1c\ \n- 表名 ${tab}\n" ./${tab}.txt
        cat ./${tab}.txt >> ./tt.txt
        #echo ${a//+/|}>./${tab}.txt
done

```
