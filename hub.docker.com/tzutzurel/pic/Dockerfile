FROM jenkins:1.625.3

MAINTAINER IOP

# if we want to install via apt
USER root

# install apt-transport-https
RUN apt-get update && apt-get install -y apt-transport-https

# Add Docker entry
RUN apt-key adv --keyserver hkp://p80.pool.sks-keyservers.net:80 --recv-keys 58118E89F3A912897C070ADBF76221572C52609D \
  && echo "deb https://apt.dockerproject.org/repo debian-jessie main" >> /etc/apt/sources.list.d/docker.list

# install docker-engine maven npm sudo
RUN apt-get update && apt-get install -y docker-engine maven npm sudo && rm -rf /var/lib/apt/lists/*

# ln node -> nodejs
RUN ln -s /usr/bin/nodejs /usr/bin/node

# install bower gulp
RUN npm install -g bower gulp

# run jenkins sudo without password
RUN echo "jenkins ALL=(ALL) NOPASSWD:ALL" >> /etc/sudoers.d/jenkins

# drop back to the regular jenkins user - good practice
USER jenkins
