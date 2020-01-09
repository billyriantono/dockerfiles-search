FROM ubuntu

#
RUN apt-get update \
  && apt-get -y install sudo \
  && apt-get -y install nodejs-legacy \
  && apt-get -y install npm

# Install Java
RUN apt-get -y -q install default-jdk

# Install Galen Framework
RUN sudo npm install -g galenframework-cli
