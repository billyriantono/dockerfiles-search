FROM node:alpine
WORKDIR /sky-remote-web
RUN apk add --update git && \
  rm -rf /tmp/* /var/cache/apk/*
RUN git clone https://github.com/davidjtipping/sky-remote-web.git . && \
  npm install
EXPOSE 27592
CMD ["node","/sky-remote-web/sky-remote-web.js","--hostname=localhost","--port=27592","--net=host"]
