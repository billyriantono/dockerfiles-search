FROM jenkins/jenkins:lts-alpine
LABEL maintainer="Eric Smalling github@ericsmalling.com"

COPY plugins.txt /usr/share/jenkins/ref/plugins.txt
RUN /usr/local/bin/install-plugins.sh < /usr/share/jenkins/ref/plugins.txt

ENV JAVA_OPTS -Djenkins.install.runSetupWizard=false

