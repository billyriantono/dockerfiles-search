FROM ubuntu:14.04
MAINTAINER Ahmed Kamal <email.ahmedkamal@googlemail.com>

RUN apt-get update && \
    apt-get install nodejs git -qqy  && \
    git clone https://github.com/azat-co/mongoui.git && \
    cd mongoui && sed -e s@"localhost"@"mongo"@g config_default.json > config.json && \
    apt-get clean all
WORKDIR /mongoui
EXPOSE 3000 3000
CMD nodejs index.js
