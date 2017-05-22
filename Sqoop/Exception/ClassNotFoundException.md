### 报错
Encountered IOException running import job: java.io.IOException: java.lang.ClassNotFoundException: org.apache.hadoop.hive.conf.HiveConf

### 解决办法
增加环境变量  
export HADOOP_CLASSPATH=$HADOOP_CLASSPATH:$HIVE_HOME/lib/*  

在sqoop-env.sh中设置HIVE_CONF_DIR 
