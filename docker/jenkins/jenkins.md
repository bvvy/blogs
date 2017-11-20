#### jenkins

1. 下载 jenkins

   1. 使用docker 安装
        ```
        地址 https://hub.docker.com/r/jenkins/jenkins/
        To use the latest LTS: docker pull jenkins/jenkins:lts
        To use the latest weekly: docker pull jenkins/jenkins
        ```
   2. 使用文件启动
       
    
2. 用法　
    
     地址　https://github.com/jenkinsci/docker/blob/master/README.md
     
        docker run -p 8080:8080 -p 50000:50000 jenkins/jenkins:lts
        
        配置信息，都会存在/var/jenkins_home中
        docker run -p 8080:8080 -p 50000:50000 -v jenkins_home:/var/jenkins_home jenkins/jenkins:lts
        