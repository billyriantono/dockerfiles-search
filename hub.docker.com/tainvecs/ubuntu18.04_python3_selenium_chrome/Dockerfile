

# Ubuntu:18.04
# VERSION 1.2.1


FROM ubuntu:18.04

MAINTAINER Chin-Ho, Lin <tainvecs@gmail.com>


USER root
RUN apt-get update && apt-get install -y sudo

# temporary packages
RUN sudo apt-get install -y unzip curl

# install locales and set locale to utf-8
RUN sudo apt-get -y install locales \
    && dpkg-reconfigure -f noninteractive locales \
    && sudo locale-gen en_US.UTF-8 \
    && echo "export LANG=en_US.UTF-8" >> ~/.bashrc \
    && echo "export LANGUAGE=en_US.UTF-8" >> ~/.bashrc \
    && echo "export LC_ALL=en_US.UTF-8" >> ~/.bashrc

# install python3 and selenium
RUN sudo apt-get -y install python3 python3-dev python3-pip build-essential \
    && sudo pip3 install --upgrade pip \
    && sudo pip3 install selenium \
    && echo "alias python='python3'" >> ~/.bashrc

# install google-chrome-stable
RUN sudo apt-get install -y wget \
    && wget -q -O - https://dl-ssl.google.com/linux/linux_signing_key.pub | sudo apt-key add - \
    && sudo sh -c 'echo "deb [arch=amd64] http://dl.google.com/linux/chrome/deb/ stable main" >> /etc/apt/sources.list.d/google.list' \
    && sudo apt-get -y update \
    && sudo apt-get install -y google-chrome-stable

# install chromedriver
RUN wget http://chromedriver.storage.googleapis.com/`curl -sS chromedriver.storage.googleapis.com/LATEST_RELEASE`/chromedriver_linux64.zip \
    -O /tmp/chromedriver.zip \
    && unzip /tmp/chromedriver.zip chromedriver -d /usr/local/bin/

# uninstall and remove temporary packages
RUN sudo apt-get remove -y unzip curl \
    && rm /tmp/chromedriver.zip

ENTRYPOINT ["/bin/bash"]
