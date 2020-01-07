FROM node:dubnium

# Setup
#RUN apt-get update && apt-get install apt-transport-https curl sudo wget  -y

RUN apt-get install wget -y

#RUN cd /opt \
#    wget https://yarnpkg.com/latest.tar.gz \
#    tar zvxf latest.tar.gz \
#	ln -s /opt/yarn-v1.0.1/dist/bin/yarn /usr/local/bin/yarn

# Chrome
RUN wget -q -O - https://dl-ssl.google.com/linux/linux_signing_key.pub | apt-key add -
RUN echo "deb http://dl.google.com/linux/chrome/deb/ stable main" >> /etc/apt/sources.list

# Yarn
#RUN curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | apt-key add -
#RUN echo "deb https://dl.yarnpkg.com/debian/ stable main" | tee /etc/apt/sources.list.d/yarn.list

RUN apt-get update
RUN apt-get install python-setuptools python-dev build-essential google-chrome-stable -y
RUN apt-get clean

RUN npm install -g yarn@1.19.0 typescript@~3.4.5
RUN npm i -g phantomjs-prebuilt --unsafe-perm --silent

RUN yarn add global npm@6.9.0
RUN yarn add global @angular/cli@^8.0.0
RUN yarn add global node-sass@4.5.3

RUN curl -O https://bootstrap.pypa.io/get-pip.py
RUN python get-pip.py
RUN pip install awscli