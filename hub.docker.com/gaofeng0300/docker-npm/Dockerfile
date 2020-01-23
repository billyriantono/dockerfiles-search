FROM verdaccio/verdaccio:4 as base

USER root

RUN npm i pm2 -g

ADD conf/config.yaml /verdaccio/conf/config.yaml