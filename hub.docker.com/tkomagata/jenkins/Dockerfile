FROM jenkins/jenkins:lts-alpine

# Disable Initial Setup Wizard
ENV JAVA_OPTS="-Djenkins.install.runSetupWizard=false"

# Install suggested plugins
USER root

COPY plugins.txt /usr/share/jenkins/ref/plugins.txt
RUN /usr/local/bin/install-plugins.sh < /usr/share/jenkins/ref/plugins.txt

# Set default user of container
USER jenkins 
