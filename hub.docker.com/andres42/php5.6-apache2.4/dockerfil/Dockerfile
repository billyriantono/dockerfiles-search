FROM ubuntu:14.04
MAINTAINER Andrei Coman <comandrei@gmail.com>
COPY copyables /
ADD https://dl.google.com/linux/linux_signing_key.pub /tmp/
RUN apt-key add /tmp/linux_signing_key.pub && apt-get -qq update
RUN DEBIAN_FRONTEND=noninteractive apt-get install -y -qq xvfb google-chrome-stable build-essential python-dev python-virtualenv python-pip unzip
RUN wget -O /tmp/chromedriver.zip http://chromedriver.storage.googleapis.com/2.21/chromedriver_linux64.zip && unzip /tmp/chromedriver.zip chromedriver -d /usr/local/bin/
COPY chrome_launcher.sh /opt/google/chrome/google-chrome
# Cleanup
RUN apt-get clean
RUN rm -rf /var/cache/*
RUN rm -rf /tmp/*
