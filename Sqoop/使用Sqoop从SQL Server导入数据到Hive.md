1.首先要下载SQL Server JDBC驱动包https://msdn.microsoft.com/zh-cn/library/mt683464.aspx  

2.将下载好的JDBC驱动包解压，并将sqljdbcXX.jar文件放置SQOOP_HOME/lib目录下(XX为版本号)  

3.使用下面命令进行数据导入
```
sqoop import \
--connect 'jdbc:sqlserver://10.96.227.234;database=XXXX' \
--username XX \
--password XXXX \
--query "SELECT * FROM XXXX WHERE \$CONDITIONS" \
--target-dir /XXXX \
--hive-import \
--create-hive-table \
--hive-table XXXX \
--num-mappers 1
```
或者
```
sqoop import \
--connect 'jdbc:sqlserver://10.96.227.234;username=XX;password=XXXX;database=XXXX' \
--query "SELECT * FROM XXXX WHERE ID>10000 and \$CONDITIONS" \
--target-dir /XXXX \
--hive-import \
--hive-table XXXX \
--split-by ID \
--num-mappers 2
```  

注意：  
1. 其中第一次导入数据时，如果Hive中没有对应的表，可以加上--create-hive-table选项，Hive会自动创建与导入表对应的表，并将数据导入。如果Hive表中已经有对应的表，该选项不需要带。
2. 选项--query中where条件必须要带\$CONDITIONS，包括\，否则会报错。但是在使用Sqoop中的--options-file选项时，--query中的where条件就只能使用$CONDITIONS，不需要带\，带了会报错。
3. --num-mappers中的数字为1时，不需要带--split-by选项，如果不为1时，必须带--split-by选项。--split-by选项后为字段类型，指的是sqoop按照什么字段进行任务切分。且字段只能指定为数字类型，否则会报错。
4. --hive-table指定为Hive表的名字，如果不指定默认是和SQL Server表同名。  

Sqoop的--options-file选项使用方式如下，并且文件的格式必须如下，否则会报错：
```
import

--connect
'jdbc:sqlserver://10.96.227.234;database=INFRASTRUCTURE'

--username
sa

--password
Password01!

--query
'SELECT * FROM INFRASTRUCTURE.SysDictionary WHERE $CONDITIONS'

--target-dir
/death/out16

--hive-import

--create-hive-table

--hive-table
SysDictionary

--split-by
ID

--num-mappers
2
```
