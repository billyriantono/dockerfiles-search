FROM amazonlinux:1
RUN yum -y install git vim
RUN yum -y install  java-1.8.0-openjdk-devel.x86_64
RUN yum -y install tomcat8 tomcat8-webapps tomcat-admin-webapps tomcat8-docs-webapp
RUN mkdir /home/sharefolder
EXPOSE 8080