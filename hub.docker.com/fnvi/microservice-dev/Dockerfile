FROM node:alpine

EXPOSE 3000

ENV NODE_ENV debug

ENV port 3000

COPY healthcheck.js /usr/src/

HEALTHCHECK --interval=20s --timeout=20s --start-period=30s CMD node /usr/src/healthcheck

RUN npm i -g nodemon

WORKDIR /usr/src/app

ENTRYPOINT nodemon -L --delay 5