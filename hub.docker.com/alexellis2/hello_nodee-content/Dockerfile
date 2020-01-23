FROM jenkins/jenkins:lts
USER root
RUN apt-get update
RUN apt-get install -y apt-transport-https ca-certificates curl gnupg2 software-properties-common
RUN curl -fsSL https://download.docker.com/linux/debian/gpg | apt-key add -
RUN add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/debian $(lsb_release -cs) stable"
RUN apt-get update
RUN apt-get install -y docker-ce=17.12.0~ce-0~debian

# for main web interface: 
EXPOSE 8080
# will be used by attached slave agents:
EXPOSE 50000

# Jenkins home directory is a volume, so configuration and build history
# can be persisted and survive image upgrades 
VOLUME /var/jenkins_home
