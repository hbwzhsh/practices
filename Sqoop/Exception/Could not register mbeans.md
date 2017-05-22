### 运行Sqoop时报以下错误 
main ERROR Could not register mbeans java.security.AccessControlException: access denied ("javax.management.MBeanTrustPermission" "register")   

### 解决方案  
修改$JAVA_HOME/jre/lib/security/java.policy文件  
添加如下内容：  
permission javax.management.MBeanTrustPermission "register";
