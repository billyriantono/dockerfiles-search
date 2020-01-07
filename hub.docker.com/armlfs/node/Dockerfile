FROM node:boron
RUN npm install -g ionic
ADD https://github.com/krallin/tini/releases/download/v0.14.0/tini /sbin/tini
RUN chmod 755 /sbin/tini
WORKDIR /mnt
