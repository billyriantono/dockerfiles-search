FROM jenkins/jenkins:2.128

ENV ADMIN_PASSWORD ""
ENV JAVA_OPTS="-Djenkins.install.runSetupWizard=false"
ENV JENKINS_OPTS="--prefix=/jenkins"

COPY scripts /usr/share/jenkins/ref/init.groovy.d/

#Install plugins
COPY plugins.txt /usr/share/jenkins/ref/plugins.txt
RUN /usr/local/bin/install-plugins.sh < /usr/share/jenkins/ref/plugins.txt