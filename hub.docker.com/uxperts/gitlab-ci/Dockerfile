FROM node:latest
RUN apt-get -qy update && apt-get install -qy rsync openssh-client
RUN curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | apt-key add -
RUN echo "deb http://dl.yarnpkg.com/debian/ stable main" | tee /etc/apt/sources.list.d/yarn.list
RUN apt-get -qy update && apt-get install -qy yarn 
RUN mkdir -p /root/.ssh
COPY config /root/.ssh/config
