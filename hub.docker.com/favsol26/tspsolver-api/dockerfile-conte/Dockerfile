FROM nginx:alpine

WORKDIR /usr/share/nginx/html
RUN apk add --update nodejs nodejs-npm git
RUN npm install -g bower gulp
RUN git clone https://github.com/plouc/thumbor-toy.git && mv thumbor-toy/* .; rm -r thumbor-toy
RUN npm install && cp sample/config.js ./config.js
RUN gulp
EXPOSE 80