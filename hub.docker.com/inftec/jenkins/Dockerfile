FROM jenkinsci/blueocean:1.21.0
MAINTAINER Fabian Gut <fabian.gut@inftec.ch>, InfTec GmbH

USER jenkins
COPY plugins.txt /usr/share/jenkins/ref/plugins.txt
RUN /usr/local/bin/install-plugins.sh < /usr/share/jenkins/ref/plugins.txt
