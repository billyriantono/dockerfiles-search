FROM maven:3-jdk-8-slim

RUN apt-get update -y 
RUN apt-get -y --no-install-recommends install dumb-init gnupg wget ca-certificates apt-transport-https ttf-wqy-zenhei 
       
# Install Google Chrome
RUN wget -q -O - https://dl-ssl.google.com/linux/linux_signing_key.pub | apt-key add -
RUN sh -c 'echo "deb [arch=amd64] http://dl.google.com/linux/chrome/deb/ stable main" >> /etc/apt/sources.list.d/google.list'
RUN apt-get update 
RUN apt-get install -y --no-install-recommends google-chrome-stable
RUN apt-get clean autoclean autoremove -y 
RUN rm -rf /var/lib/apt/lists/* /var/cache/apt/*

ENV IS_DOCKER true
