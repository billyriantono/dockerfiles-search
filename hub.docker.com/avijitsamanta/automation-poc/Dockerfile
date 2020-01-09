#FROM ubuntu:16.04
FROM ubuntu
MAINTAINER Avijit Samanta

# Update and install s/w
RUN apt-get update

# Install a Desktop and VNC Server
# Refer to https://linode.com/docs/applications/remote-desktop/install-vnc-on-ubuntu-16-04
#RUN apt-get --yes --force-yes install --no-install-recommends ubuntu-desktop gnome-panel gnome-settings-daemon metacity nautilus gnome-terminal

# --------------- Another way of VNC Server installation ----
RUN apt-get --yes --force-yes install -y python-pip python-dev build-essential 
RUN pip install --upgrade pip 
RUN pip install --upgrade virtualenv 

#Upgrade pip, install Git & VNC 	
RUN pip install --upgrade pip \
        && apt-get update \
        && apt-get install -y git x11vnc
# -----------------------------------------------------------

RUN apt-get install -y openjdk-8-jdk git wget unzip curl 
RUN apt-get install -y git maven
RUN apt-get install -y xvfb libxi6 libgconf-2-4
#RUN apt-get install vnc4server

#  Install Chrome driver for Ubuntu
RUN wget -N http://chromedriver.storage.googleapis.com/2.33/chromedriver_linux64.zip
RUN unzip chromedriver_linux64.zip -d /usr/local/share
RUN rm chromedriver_linux64.zip
RUN chmod +x /usr/local/share/chromedriver
RUN ln -s /usr/local/share/chromedriver /usr/local/bin/chromedriver
RUN ln -s /usr/local/share/chromedriver /usr/bin/chromedriver

# Install Chrome
RUN curl -sS -o - https://dl-ssl.google.com/linux/linux_signing_key.pub | apt-key add -
RUN echo "deb http://dl.google.com/linux/chrome/deb/ stable main" >> /etc/apt/sources.list.d/google-chrome.list
RUN apt-get -yqq update
RUN apt-get -yqq install google-chrome-stable
RUN rm -rf /var/lib/apt/lists/*

# Clone Git repo and build/execute automation package
RUN git clone -b base --single-branch https://github.com/avijit-samanta/selenium-bdd-poc.git
WORKDIR selenium-bdd-poc
RUN mvn install
