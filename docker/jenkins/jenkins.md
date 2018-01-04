#### jenkins

1. 下载 jenkins

   1. 使用docker 安装jenkins/blueocean
        
        ```
         docker run \
           --rm \
           -d \
           -p 8080:8080 \
           -v jenkins-data:/var/jenkins_home \
           -v /var/run/docker.sock:/var/run/docker.sock \
           -v "%HOMEPATH%":/home
           jenkinsci/blueocean
        
        ```
    
2. 用法

   2.1 访问localhost:8080查看启动
   
   2.2 命令 docker logs <container name >查看密码
   
   2.3 安装推荐的插件
   
   2.4 使用github fork  https://github.com/YOUR-GITHUB-ACCOUNT-NAME/simple-java-maven-app
   
   2.5 把git项目clone 到本地
   
   2.6 然后捏...
   
   
   
    
            