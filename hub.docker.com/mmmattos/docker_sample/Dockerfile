FROM node:latest
ENV REFRESHED_AT 2013-08-26
MAINTAINER Miguel Miranda de Mattos "miguel.mattos@mmmattos.net"
WORKDIR /home/app
COPY . /home/app
RUN \
    npm install -g bower && \
    npm install && \
    bower install --config.interactive=false --allow-root
EXPOSE 9000
CMD ["node", "server/app.js"]
