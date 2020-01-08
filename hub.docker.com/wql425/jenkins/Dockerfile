FROM wql425/gradle:latest
MAINTAINER Darrell
LABEL name="jenkins" version="2.193" description="Jenkins"

# Install Git Client
RUN yum install -y git && yum clean all

# 数据目录
ENV JENKINS_HOME=/var/jenkins_home
WORKDIR /

RUN curl -o jenkins.war http://ftp-nyc.osuosl.org/pub/jenkins/war/2.193/jenkins.war

VOLUME /var/jenkins_home
EXPOSE 8080
CMD ["java","-jar","jenkins.war"]
