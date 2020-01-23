FROM node:alpine

MAINTAINER David Chen <david@davidchen.blog>

RUN npm install --prefix gitfiles -g https://github.com/citronneur/mstsc.js/tarball/master

WORKDIR /gitfiles/lib/node_modules/mstsc.js

EXPOSE 9250 

CMD ["node", "server.js"]
