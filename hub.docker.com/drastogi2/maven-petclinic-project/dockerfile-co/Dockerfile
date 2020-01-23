FROM       openjdk
MAINTAINER Gabriel Bratescu <gabriel.bratescu@gmail.com>

RUN apt-get install -y curl
RUN curl -sL https://deb.nodesource.com/setup_6.x | bash -
RUN apt-get install -y nodejs python g++ build-essential && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

RUN npm install -g yo
RUN npm install -g tslint
RUN npm install -g yarn
