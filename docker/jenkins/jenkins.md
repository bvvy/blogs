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
        
        配置信息，插件信息都会存在/var/jenkins_home中
        docker run -d -p 8080:8080 -p 50000:50000 -v /home/jenkins_home:/var/jenkins_home jenkins/jenkins:lts
        docker run \
          --rm \
          -u root \
          -p 8080:8080 \
          -v /home/bvvy/jenkins_home:/var/jenkins_home \
          -v /var/run/docker.sock:/var/run/docker.sock \
          -v "$HOME":/home \
          jenkinsci/blueocean
        