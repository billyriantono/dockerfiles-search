FROM node:10

MAINTAINER Franck Delage <franck@web82.fr>

RUN apt-get update && apt-get install -y apt-transport-https
RUN echo "deb [arch=amd64] http://dl.google.com/linux/chrome/deb/ stable main" >> /etc/apt/sources.list.d/google-chrome.list
RUN wget -q -O - https://dl-ssl.google.com/linux/linux_signing_key.pub | apt-key add -
RUN curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | apt-key add -
RUN echo "deb https://dl.yarnpkg.com/debian/ stable main" | tee /etc/apt/sources.list.d/yarn.list
RUN apt-get update && apt-get install -qq -y --no-install-recommends curl vim git build-essential google-chrome-stable yarn

RUN yarn global add @angular/cli@7.0.3
RUN yarn add @angular/cli@7.0.3
RUN yarn add typescript
RUN ng config -g cli.packageManager yarn
