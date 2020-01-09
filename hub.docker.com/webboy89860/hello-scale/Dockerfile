FROM node:6-wheezy
MAINTAINER jamlee<jamlee@jamlee.cn>
WORKDIR /usr/src/app
ADD app/ /usr/src/app/
ADD bin/  /usr/bin/

ENTRYPOINT ["node", "/usr/src/app/app.js"]
