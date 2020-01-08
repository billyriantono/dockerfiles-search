FROM docker.io/ubuntu:18.10 
MAINTAINER Viktor Horvath <support@reaction-engine.org>

# create folders for the reaction components
RUN mkdir /local && mkdir /local/reaction && mkdir /local/reaction/install && mkdir /local/reaction/install/engine && mkdir /local/reaction/engine && mkdir /local/reaction/engine/log

# update the repositories and install vim, wget, unzip amd curl
RUN apt-get update -y && apt-get install -y vim wget unzip curl

# install sudo && change the pwd of root
RUN apt-get install -y sudo && echo root:root | chpasswd

#############################################################################
#                   1. install engine
#############################################################################

# installing jdk
RUN apt-get -y install openjdk-11-jdk
# creating Linux user for Tomcat
RUN groupadd tomcat && useradd -s /bin/false -g tomcat -d /opt/tomcat tomcat
# getting the ZIP and unzip it
RUN wget https://archive.apache.org/dist/tomcat/tomcat-9/v9.0.8/bin/apache-tomcat-9.0.8.tar.gz -P /tmp/ && mkdir /opt/tomcat && tar xzvf /tmp/apache-tomcat-9.0.8.tar.gz -C /opt/tomcat --strip-components=1 && rm -f /tmp/apache-tomcat-9.0.8.tar.gz
# setting the permissions
RUN cd /opt/tomcat && chgrp -R tomcat /opt/tomcat && chmod -R g+r conf && chmod g+x conf && chown -R tomcat webapps/ work/ temp/ logs/
# setting write permission to /local/reaction/engine/log for tomcat user and root group
RUN chown -R tomcat /local/reaction/engine/log && chmod g+w /local/reaction/engine/log

# install Oracle client
RUN apt-get -y install libaio1
RUN wget https://bitbucket.org/ric_flair_wcw/reaction-storage-v1_1/downloads/oracle-instantclient12.2-basic-12.2.0.1.0-1.x86_64.rpm -P /local/reaction/install/management_app
RUN apt-get -y install alien && alien -i /local/reaction/install/management_app/oracle-instantclient12.2-basic-12.2.0.1.0-1.x86_64.rpm

# downloading the WAR, config file, log config file
RUN wget https://bitbucket.org/ric_flair_wcw/reaction-storage-v1_1/downloads/reaction-engine-tomcat-1.1.war -P /local/reaction/install/engine
RUN wget https://bitbucket.org/ric_flair_wcw/reaction-storage-v1_1/downloads/reaction-engine-config-1.1.zip -P /local/reaction/install/engine
RUN unzip /local/reaction/install/engine/reaction-engine-config-1.1.zip -d /local/reaction/engine

# copying the WAR file to tomcat/webapps
RUN mv /local/reaction/install/engine/reaction-engine-tomcat-1.1.war /local/reaction/install/engine/reaction-engine.war && chmod a+w /local/reaction/install/engine/reaction-engine.war && cp /local/reaction/install/engine/reaction-engine.war /opt/tomcat/webapps
# setting the starting parameter of reaction engine to tomcat (altering /opt/tomcat/bin/setenv.sh)
RUN touch /opt/tomcat/bin/setenv.sh && echo 'CATALINA_OPTS="-Dspring.profiles.active=threadPool -Dspring.config.location=/local/reaction/engine/reaction-engine-application.yml -Dreaction.logback.config=/local/reaction/engine/logback-include.xml"' >> /opt/tomcat/bin/setenv.sh && chmod a+x /opt/tomcat/bin/setenv.sh
# altering the reaction engine config file (setting the location of the credentials file)
RUN sed -i "s|credentials_file: file:/local/reaction/engine/security/credentials|credentials_file: file:/local/reaction/engine/credentials|g" /local/reaction/engine/reaction-engine-application.yml
# setting the log file location
RUN sed -i "s|<file>reaction-engine.log</file>|<file>/local/reaction/engine/log/reaction-engine.log</file>|g" /local/reaction/engine/logback-include.xml
# setting the credentials of worker and management app web for authentication
RUN touch /local/reaction/engine/credentials && echo "localhost=f0dedb78-3eb6-4a56-8428-e8e40584a01c" >> /local/reaction/engine/credentials && echo "reaction-management-web-app=e5574bf1-13c5-476a-b1d3-500bc640564d" >> /local/reaction/engine/credentials

HEALTHCHECK --interval=10s --retries=10 CMD curl --fail curl --fail http://localhost:8080/reaction-engine/status

CMD ["/opt/tomcat/bin/catalina.sh", "run"]

EXPOSE 8080
