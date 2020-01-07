FROM node:12.1.0-stretch

LABEL maintainer="cedric.penas@gmail.com"

RUN apt-get update \
    && apt-get install -y ruby-full rubygems curl wget \
    && rm -rf /var/lib/apt/lists/*

RUN gem install sass

WORKDIR /data

CMD ["bash"]
