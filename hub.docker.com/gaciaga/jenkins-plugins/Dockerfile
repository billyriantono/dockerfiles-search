FROM gaciaga/jenkins-docker:2.46.1-alpine

COPY executors.groovy /usr/share/jenkins/ref/init.groovy.d/executors.groovy

COPY plugins-list /usr/share/jenkins/ref/
RUN /usr/local/bin/install-plugins.sh `cat /usr/share/jenkins/ref/plugins-list`