FROM jenkins/jenkins:lts

LABEL maintainer="Michael Huber"

# Installing plugins
COPY plugins.txt /usr/share/jenkins/ref/plugins.txt
RUN /usr/local/bin/install-plugins.sh < /usr/share/jenkins/ref/plugins.txt

# Turning off initial setup
ENV JAVA_OPTS="-Djenkins.install.runSetupWizard=false"