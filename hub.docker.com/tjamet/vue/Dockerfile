FROM node:alpine

RUN npm install -g vue-cli git
ENV HOME=/home/
ENTRYPOINT ["vue"]
LABEL io.whalebrew.config.volumes='["~/.home.vue:/home"]'
