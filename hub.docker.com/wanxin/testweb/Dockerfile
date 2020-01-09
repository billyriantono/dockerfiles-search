# Base image to use, this must be set as the first line
FROM hub.c.163.com/public/tomcat:7.0.28

# Maintainer: docker_user <docker_user at email.com> (@docker_user)
MAINTAINER wanxin <258621580@qq.com>



# put web package
RUN rm -rf /var/lib/tomcat7/webapps/*
COPY war /var/lib/tomcat7/webapps

# Commands when creating a new container
# EXPOSE 8080
# ENTRYPOINT /opt/apache-tomcat-8.5.13/bin/startup.sh && tail -F /opt/apache-tomcat-8.5.13/logs/catalina.out
