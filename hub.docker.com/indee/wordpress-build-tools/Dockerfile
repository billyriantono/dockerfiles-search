FROM indee/wordpress:latest

RUN curl -sL https://deb.nodesource.com/setup_4.x | sudo -E bash - \
    && apt-get update \
    && apt-get install -y nodejs git build-essential unzip

RUN npm install -g \
    gulp \
    bower \
    grunt-cli
