# 调试指令

## Java

### Tomcat

修改`$CATALINA_HOME/bin/startup.sh`最后一行

```java
exec "$PRGDIR"/"$EXECUTABLE" jpda start "$@" 
```

修改jpda端口在`catalina.sh`中

```java
JPDA_APPDESS=8000
```

### Springboot

```java
java -jar -Xdebug -Xrunjdwp:transport=dt_socket,server=y,suspend=n,address=5005 test-tool.jar
```

## Python

