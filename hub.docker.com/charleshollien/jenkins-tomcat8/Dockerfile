FROM ubuntu:18.04
ENV JENKINS_HOME /jenkins
ENV DEBIAN_FRONTEND noninteractive
#Instal and configure Tomcat	
RUN apt-get update && apt-get install openjdk-8-jre-headless wget -y && apt-get install tomcat8 -y && \ 
mkdir -p /usr/share/tomcat8 && ln -s /etc/tomcat8 /usr/share/tomcat8/conf && mkdir -p /usr/share/tomcat8/temp && \
mkdir -p /usr/share/tomcat8/webapps/ && chown tomcat8:tomcat8 -R /usr/share/tomcat8 && \
mkdir -p /jenkins && chown tomcat8:tomcat8 /jenkins/ -R && \
chown tomcat8:tomcat8 /var/lib/tomcat8 -R 
#Install build tools
RUN apt-get install build-essential -y
#Install Devops Tools
RUN apt-get install python-pip git chef vagrant -y && pip install ansible
WORKDIR /usr/bin/
RUN curl -LO https://storage.googleapis.com/kubernetes-release/release/$(curl -s https://storage.googleapis.com/kubernetes-release/release/stable.txt)/bin/linux/amd64/kubectl
WORKDIR /usr/share/tomcat8/webapps/
RUN wget http://mirrors.jenkins.io/war-stable/latest/jenkins.war
VOLUME /jenkins
USER tomcat8
EXPOSE 8080
CMD /usr/share/tomcat8/bin/catalina.sh run
