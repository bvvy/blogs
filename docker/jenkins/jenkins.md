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
           jenkinsci/blueocean
        
        ```
   2. 使用文件启动
       
    
2. 用法　
    
            