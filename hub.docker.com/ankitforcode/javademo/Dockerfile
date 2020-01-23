FROM ubuntu:trusty

#adds the add-apt-repo tool
RUN apt-get update -qq && \
	apt-get install -y software-properties-common && \
	apt-get clean

#install oracle java 8
RUN add-apt-repository ppa:webupd8team/java
RUN apt-get update
RUN echo oracle-java8-installer shared/accepted-oracle-license-v1-1 select true | /usr/bin/debconf-set-selections
RUN apt-get install -y oracle-java8-installer

#install tomcat
WORKDIR /opt
RUN wget http://archive.apache.org/dist/tomcat/tomcat-8/v8.0.26/bin/apache-tomcat-8.0.26.tar.gz
RUN tar -zxvf apache-tomcat-8.0.26.tar.gz
RUN mv apache-tomcat-8.0.26 tomcat

#tomcat admin credentials
ENV TOMCAT_PASS admin
ENV CATALINA_HOME /opt/tomcat

EXPOSE 8080

ADD create_tomcat_admin_user.sh /create_tomcat_admin_user.sh

ADD run.sh /run.sh
RUN chmod +x /*.sh

CMD ["/run.sh"]
