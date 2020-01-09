FROM 'jenkins/jenkins-experimental:latest-jdk11'
WORKDIR /
USER root
ENV DEBIAN_FRONTEND=noninteractive
RUN apt update
RUN apt install jmeter -q -y 

WORKDIR /tmp
ARG GRADLE_VERSION=4.10.3
ARG GRADLE_DIR=gradle-$GRADLE_VERSION
ARG GRADLE_INSTALL=/opt/gradle/latest
ARG GRADLE_FILE=$GRADLE_DIR-bin.zip
ARG CHECKSUM_FILE=$GRADLE_FILE.sha256
RUN /usr/bin/wget -O $GRADLE_FILE https://services.gradle.org/distributions/$GRADLE_FILE
RUN /usr/bin/wget -O $CHECKSUM_FILE https://downloads.gradle.org/distributions/$GRADLE_FILE.sha256
RUN echo " *$GRADLE_FILE" >> $CHECKSUM_FILE
RUN sha256sum -c $CHECKSUM_FILE
RUN unzip $GRADLE_FILE
RUN rm $GRADLE_FILE $CHECKSUM_FILE

WORKDIR /opt
RUN mkdir -p gradle
WORKDIR /opt/gradle
RUN mv /tmp/$GRADLE_DIR ./$GRADLE_VERSION
RUN ln -s /opt/gradle/$GRADLE_VERSION $GRADLE_INSTALL 
RUN chmod 755 -R /opt/gradle/latest

#USER jenkins
WORKDIR /var/jenkins_home
ENV GRADLE_HOME=$GRADLE_INSTALL
ENV PATH=$GRADLE_HOME/bin:$PATH

