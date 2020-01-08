FROM ubuntu:18.04

RUN apt-get update \
    &&  apt-get install -y curl xvfb build-essential wget nodejs npm
 
RUN wget -q -O - https://dl.google.com/linux/linux_signing_key.pub | apt-key add - \
    &&  sh -c 'echo "deb [arch=amd64] http://dl.google.com/linux/chrome/deb/ stable main" >> /etc/apt/sources.list.d/google.list' \
    &&  apt-get update \
    &&  apt-get install -y google-chrome-stable

