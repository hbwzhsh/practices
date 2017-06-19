shell中case和shift的使用比较常见，这里简单记录一下使用方法：  

### case用法  
shell中的case，相当于Java中的switch，Scala中的match，也就是一个模式匹配。具体语法如下：  
```shell
case 值 in
  模式1)
  command
  ;;

  模式2)
  command
  ;;

  ...

  模式n|模式n+1|模式n+2)
  command
  ;;

  *)
  command
  ;;
esac
```  
由上可以看出，case中可以指定多个模式，这里的模式说简单点其实就是字符串，比如file或者-file或者--file等等。下面给出一个例子：
```shell
#!/bin/bash

command=$1

case $command in
  file)
    command="I am file"
    echo $command
  ;;

  -file)
    command="I am -file"
    echo $command
  ;;

  --file)
    command="I am --file"
    echo $command
  ;;

  text|-text|--text)
    command="I am text"
    echo $command
  ;;

  *)
    echo $command
  ;;
esac
```  
模式text|-text|--text中，只要与其中一个匹配成功就算成功，逻辑或，不难理解。模式*匹配任何情况。注意，case语句只要匹配到第一个就会返回结果，不会再往下匹配。  

### shift用法  
shell中shift的做用是将shell脚本中传递的参数前移。什么意思呢？举个例子，写一个脚本testshift.sh，脚本内容如下：  
```shell
#!/bin/bash

echo $1
shift
echo $1
shift
echo $1
```  
脚本很简单，不难看出输出三次传入的第一个参数，那么三次的结果是什么？执行该脚本，传入三个参数python testshift.sh aa bb cc，三次输出的结果依次是aa、bb、cc。从输出结果就能明白shift的作用是什么。就是参数位置前移。注意每次只能移动一位，而且是顺序的向前移动。
