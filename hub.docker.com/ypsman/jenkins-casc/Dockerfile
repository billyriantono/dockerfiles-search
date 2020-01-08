# file: Dockerfile
# Author: Yves Sanderbrand <yvessander@gmail.com>

FROM jenkins/jenkins:lts
ENV JAVA_OPTS="-Djenkins.install.runSetupWizard=false -Dhudson.plugins.active_directory.ActiveDirectorySecurityRealm.forceLdaps=true"
COPY plugins.txt /usr/share/jenkins/ref/plugins.txt
COPY groovy.d/ /usr/share/jenkins/ref/init.groovy.d/
RUN /usr/local/bin/install-plugins.sh  < /usr/share/jenkins/ref/plugins.txt
