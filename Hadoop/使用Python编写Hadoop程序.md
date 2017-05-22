Hadoop版本为2.7.3  

如何使用python编写mapreduce网上有很多，这里就不说了，这里主要说的是使用python编写好mapreduce程序后如何执行，因为网上的教程版本都很老，在新版中执行可能会有问题。  

在新版的Hadoop中，执行python版的程序具体方法如下：  
```
yarn jar /usr/local/hadoop/share/hadoop/tools/lib/hadoop-streaming-2.7.3.jar \
-jobconf mapred.reduce.tasks=1 \  //可选
-mapper "python /home/hadoop/death/pyhadoop/mapper.py" \
-reducer "python /home/hadoop/death/pyhadoop/reducer.py" \
-input /XXXX/wordcount.txt \
-output /XXXX/output
```
或者
```
yarn jar /usr/local/hadoop/share/hadoop/tools/lib/hadoop-streaming-2.7.3.jar \
-jobconf mapred.reduce.tasks=1 \  //可选
-file /home/hadoop/death/pyhadoop/mapper.py \
-mapper "python mapper.py" \
-file /home/hadoop/death/pyhadoop/reducer.py
-reducer "python reducer.py" \
-input /XXXX/wordcount.txt \
-output /XXXX/output
```
