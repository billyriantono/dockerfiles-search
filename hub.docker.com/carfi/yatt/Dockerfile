FROM digitallyseamless/nodejs-bower-grunt:latest

MAINTAINER Davide Carfi <davide@carfi.org>

WORKDIR /home/yatt

COPY . /home/yatt

RUN npm install \
    && apt-get update \
    && apt-get -y install ruby-compass \
    && bower install --config.interactive=false --allow-root \
    && grunt

EXPOSE 9000

CMD ["node", "server/yatt.js"]
