FROM jenkins/jenkins

USER root

#COPY config.xml /tmp/config.xml
RUN wget https://github.com/evertonhideo/jenkins/archive/master.zip -P /tmp \
    && unzip /tmp/master.zip -d /tmp
COPY init.groovy /usr/share/jenkins/ref/init.groovy.d/init.groovy

USER jenkins