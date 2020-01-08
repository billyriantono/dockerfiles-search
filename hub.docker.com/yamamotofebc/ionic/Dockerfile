FROM node:7

# for maintainer label
MAINTAINER Kazumichi Yamamoto <yamamoto.febc@gmail.com>
LABEL maintainer="Kazumichi Yamamoto <yamamoto.febc@gmail.com>"

# for whalebrew label
LABEL io.whalebrew.config.ports '["8100:8100"]'

# install ionic + cordova
RUN npm install -g cordova ionic

WORKDIR /workdir
EXPOSE 8100
ENTRYPOINT ["ionic"]
