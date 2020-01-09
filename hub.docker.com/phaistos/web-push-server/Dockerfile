FROM node:alpine
MAINTAINER Robert Krambovitis <rkrambovitis@gmail.com>

RUN adduser -D push
USER push
WORKDIR /home/push
ADD index.js package.json /home/push/
RUN npm install

CMD node index.js
