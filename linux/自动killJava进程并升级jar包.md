# 自动 kill Java 进程，并升级 jar 包
```bash
$ [root@beluag-x project]# cat reload_inner.sh 
#!/bin/bash

PROJECTINNERPID=`ps aux | grep project-inner-906.jar | grep -v grep | awk '{print $2}'`

if [ $PROJECTINNERPID ];then
  echo "kill INNER service  progress id : $PROJECTINNERPID"
  kill -s 15 $PROJECTINNERPID
fi

sleep 3

JAVA_OPTS="-Xms512m -Xmx512m -XX:MetaspaceSize=200m -XX:MaxMetaspaceSize=200m -Dfile.encoding=utf-8"

JAVA_OPTS="$JAVA_OPTS -XX:+UseG1GC -XX:MaxGCPauseMillis=200 -XX:+UseGCOverheadLimit -XX:+ExplicitGCInvokesConcurrent"


nohup java ${JAVA_OPTS} -jar project-inner-9005.jar --spring.config.location=./config/project-inner.yml > /dev/null 2>&1 &
```
