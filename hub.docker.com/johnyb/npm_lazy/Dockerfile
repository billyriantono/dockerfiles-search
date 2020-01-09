FROM node

MAINTAINER Julian Bäume <julian@svg4all.de>

EXPOSE 8080

RUN npm install --silent -g npm_lazy && \
    npm_lazy --init > /etc/npm_lazy.js

ENTRYPOINT npm_lazy
CMD ["-c ", "/etc/npm_lazy.js"]

