#定制jenkens，并支持直接访问宿主主机docker

FROM jenkins/jenkins:centos
#注入docker客户端程序
COPY docker /usr/bin/docker
COPY docker-compose /usr/local/bin/docker-compose
USER root
#设置权限
RUN chmod +x /usr/bin/docker && chmod +x /usr/local/bin/docker-compose
USER jenkins
#安装常用插件 blueocean(新界面插件) ssh(执行远程ssh命令) localization-zh-cn(简体中文支持) workflow-aggregator(工作流插件) email-ext(邮件扩展插件) git(GIT插件)
RUN install-plugins.sh blueocean ssh localization-zh-cn workflow-aggregator email-ext git
#设置docker主机地址（不能使用localhost与127.0.0.1）
ENV DOCKER_HOST tcp://192.168.0.118:2375