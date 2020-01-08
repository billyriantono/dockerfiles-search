FROM node:6.5

RUN mkdir /src

ENV GIT_DIR=/src

RUN npm install -g pm2

RUN npm install -g node-sass
RUN npm install -g node-gyp
RUN npm rebuild -g node-sass

RUN npm install -g gulp-cli
RUN npm install -g bower

WORKDIR /src

# Setup startup script
COPY docker-entrypoint.sh /docker-entrypoint.sh
RUN chmod +x /docker-entrypoint.sh
ENTRYPOINT ["/docker-entrypoint.sh"]