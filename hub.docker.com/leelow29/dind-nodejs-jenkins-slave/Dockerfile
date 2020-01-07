FROM tehranian/dind-jenkins-slave
MAINTAINER leelow <leo.lozach@gmail.com>

# Install tools to build nodejs project
RUN apt-get update && apt-get install -y sudo g++ make python

# Add jenkins user as sudo
RUN sudo adduser jenkins sudo
RUN echo "jenkins ALL=(ALL) NOPASSWD: ALL" >> /etc/sudoers

# Install nodejs and npm
RUN curl -sL https://deb.nodesource.com/setup_6.x | sudo -E bash -
RUN sudo apt-get install -y nodejs
