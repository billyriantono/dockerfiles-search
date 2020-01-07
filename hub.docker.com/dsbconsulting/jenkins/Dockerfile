FROM jenkins:latest

# Install docker
USER root
RUN apt-get update
RUN apt-get install apt-transport-https -y
RUN apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 36A1D7869245C8950F966E92D8576A8BA88D21E9
RUN sh -c "echo deb https://get.docker.io/ubuntu docker main > /etc/apt/sources.list.d/docker.list"
RUN apt-get update
RUN apt-get install lxc-docker-1.5.0 -y

# Return rights
USER jenkins

# Attach volume
# VOLUME /var/jenkins_home:/var/jenkins_home
# VOLUME /var/cloud/devops_main/jenkins_home:/var/cloud/devops_main/jenkins_home

# Install plugins
COPY plugins.txt /plugins.txt
RUN /usr/local/bin/plugins.sh plugins.txt
ENTRYPOINT ["/usr/local/bin/jenkins.sh"]
