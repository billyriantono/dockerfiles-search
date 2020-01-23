FROM jenkins 
USER root
ARG dockerGid=999 
RUN echo "docker:x:${dockerGid}:jenkins" >> /etc/group
# 安装 docker-compose
RUN curl -L https://github.com/docker/compose/releases/download/1.16.1/docker-compose-`uname -s`-`uname -m` -o /usr/local/bin/docker-compose 
RUN chmod +x /usr/local/bin/docker-compose
