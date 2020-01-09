FROM node:latest
EXPOSE 3000
WORKDIR /host

# Install at a root level all of the basic programs needed
RUN ["apt-get", "update"]
RUN ["apt-get", "install", "-y", "sudo"]
RUN ["apt-get", "install", "-y", "dos2unix"]
RUN ["apt-get", "install", "-y", "vim"]
RUN ["apt-get", "install", "-y", "nano"]
RUN ["apt-get", "install", "-y", "tig"]
RUN ["apt-get", "install", "-y", "default-jdk"]

# Manually install Maven for 3.3.9
RUN cd /opt/ && \
    wget http://www-eu.apache.org/dist/maven/maven-3/3.3.9/binaries/apache-maven-3.3.9-bin.tar.gz && \
    tar -xvzf apache-maven-3.3.9-bin.tar.gz && \
    mv apache-maven-3.3.9 maven

ENV M2_HOME /opt/maven
ENV PATH=${M2_HOME}/bin:${PATH}

# Setup the node user to sudo group
RUN adduser node sudo
RUN echo node:node | chpasswd
ADD .bashrc /home/node/
RUN dos2unix /home/node/.bashrc
RUN chown node /home/node/.bashrc

# Switch over to node user, and set up ssh directory
USER node
RUN mkdir /home/node/.ssh
ADD config /home/node/.ssh

# Install helper scripts
RUN wget -qO- https://raw.githubusercontent.com/creationix/nvm/v0.33.2/install.sh | bash

# Install global NPM packages
# (Need to sudo each at this point so they get pulled in under the node version associated with NVM)
RUN echo "node" | sudo -S npm install -g gulp
