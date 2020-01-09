# 升级到 12 后报错：ReferenceError: primordials is not defined
FROM node:10-alpine

ENV TZ=CST-8
EXPOSE 80

RUN apk --no-cache add nginx
WORKDIR /app
CMD ["sh", "/app/start.sh"]

ADD ./ /app
RUN mv nginx.conf /etc/nginx/ && npm install && npm run compile