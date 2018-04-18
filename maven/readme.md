### maven 的一些常用操作

1. 添加本地的jar文件到本地的仓库

    ```
    mvn install:install-file 
    
    -Dfile=D:\mvn\spring-context-support-3.1.0.RELEASE.jar 
    
    -DgroupId=org.springframework 
    
    -DartifactId=spring-context-support 
    
    -Dversion=3.1.0.RELEASE 
    
    -Dpackaging=jar
    ---dfsd -df-sd 
    ```