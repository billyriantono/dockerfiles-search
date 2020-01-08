FROM qnib/dplain-init

ARG NODEJS_VER=4.5
RUN apt-get update \
 && apt-get install -y curl \
 && curl -sL https://deb.nodesource.com/setup | bash - \
 && apt-get update \
 && apt-get install -y nodejs \
 && npm install -g n \
 && n ${NODEJS_VER}
