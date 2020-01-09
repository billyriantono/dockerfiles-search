FROM ghost:latest
MAINTAINER Thomas Goddard <thomas@instamotor.com>
ONBUILD RUN npm install
ONBUILD RUN npm install --save ghost-s3-storage
ONBUILD  RUN mkdir -p content/storage && mkdir content/storage/ghost-s3
ONBUILD RUN echo "'use strict'; module.exports = require('ghost-s3-storage');" > content/storage/ghost-s3/index.js
CMD ["npm", "start"]
EXPOSE 9000
EXPOSE 8080
EXPOSE 2368
EXPOSE 80
