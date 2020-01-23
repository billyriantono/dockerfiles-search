FROM node:alpine
WORKDIR /app
RUN echo "https://mirrors.aliyun.com/alpine/latest-stable/main/" > /etc/apk/repositories
RUN apk add tzdata --update --no-cache \
  && cp /usr/share/zoneinfo/Asia/Shanghai /etc/localtime \
  && echo "Asia/Shanghai" /etc/localtime \
  && apk del tzdata
COPY . .
RUN apk add --no-cache python make g++ git \
  && npm i --production \
  && npm cache clean --force \
  && apk del python make g++ git
VOLUME /app/data
CMD node .

EXPOSE 80
EXPOSE 90/udp