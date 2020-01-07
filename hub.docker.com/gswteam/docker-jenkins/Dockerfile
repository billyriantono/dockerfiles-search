FROM jenkins:1.651.1

MAINTAINER Fabio H. G. Barbosa <fabiohbarbosa@gmail.com>

USER root

# Node.js
RUN curl -sL https://deb.nodesource.com/setup_6.x | bash -
RUN apt-get install -y nodejs

RUN npm install bower gulp pm2 nodemon babel-cli --g

# Maven
ENV MAVEN apache-maven-3.3.9
RUN wget -q http://ftp.unicamp.br/pub/apache/maven/maven-3/3.3.9/binaries/$MAVEN-bin.tar.gz -P /opt/
RUN tar -xvvzf /opt/$MAVEN-bin.tar.gz -C /opt/
RUN mv /opt/$MAVEN/ /opt/apache-maven
RUN ln -sf /opt/apache-maven/bin/mvn /usr/local/bin/mvn
RUN ln -sf /opt/apache-maven/bin/mvnDebug /usr/local/bin/mvnDebug

# Tools
RUN apt-get install -y git vim build-essential

# Timezone
COPY timezone /etc/timezone

# Clean
RUN rm -rf /opt/$MAVEN-bin.tar.gz

USER jenkins

# Jenkins
EXPOSE 8080
EXPOSE 50000

# Node server
EXPOSE 5000
