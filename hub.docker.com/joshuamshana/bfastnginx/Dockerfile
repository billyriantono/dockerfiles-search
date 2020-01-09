FROM nginx:stable-alpine

WORKDIR /web

COPY nginx.conf /etc/nginx/conf.d/default.conf
RUN apk update
RUN apk upgrade
RUN apk add unzip
RUN apk add curl
# RUN curl -sL https://deb.nodesource.com/setup_10.x | bash
# RUN apt-get install -y nodejs
# # RUN npm i -g @angular/cli
# RUN git clone https://github.com/fahamutech/BFastIDEAngularApp.git ./
# RUN git pull origin master
# RUN npm install
# RUN npm run build
# # RUN ls /web/dist/app
RUN  curl -L https://github.com/fahamutech/BFastIDEAngularApp/releases/download/v1.0.1RC/app.zip > /web/app.zip && unzip /web/app.zip
# COPY /web/app /usr/share/nginx/html/
RUN mkdir /dist
RUN cp -r /web/app /dist
# RUN apt-get purge -y git
RUN apk del unzip
RUN apk del curl
RUN rm -r /web/*
