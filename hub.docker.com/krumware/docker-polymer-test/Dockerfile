FROM node:8-stretch

# add Chrome sources
RUN apt-get install -y curl \
    && curl -sL https://dl-ssl.google.com/linux/linux_signing_key.pub | apt-key add - \
    && echo 'deb http://dl.google.com/linux/chrome/deb/ stable main' >> /etc/apt/sources.list.d/google.list

RUN apt-get update;

# install java; needed by selenium
RUN apt-get install -y \
    default-jre \
    google-chrome-stable \
    libgconf-2-4 \
    xvfb

# install web-component-tester & bower globally
RUN npm install -g npm@4 
RUN npm install -g gulpjs/gulp#4.0 gulp-cli bower polymer-cli
RUN echo '{ "allow_root": true }' > /root/.bowerrc

#try to fool google-chrome to run without sandbox - from https://github.com/printminion/polymer-tester
RUN mv /usr/bin/google-chrome /usr/bin/google-chrome-orig \
    && echo '#!/bin/bash' > /usr/bin/google-chrome \
    && echo '/usr/bin/google-chrome-orig --no-sandbox --disable-setuid-sandbox --allow-sandbox-debugging "$@"' >> /usr/bin/google-chrome  \
    && chmod +x /usr/bin/google-chrome

RUN mkdir src
WORKDIR /src