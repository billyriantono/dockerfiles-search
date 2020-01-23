FROM node:10.15.3-slim

WORKDIR /root
RUN npm install -g imagemin
RUN npm install --save-dev imagemin-keep-folder imagemin-mozjpeg imagemin-pngquant imagemin-gifsicle imagemin-svgo
COPY imagemin.js /root/imagemin.js

WORKDIR /work
ENTRYPOINT [ "node", "/root/imagemin.js" ]