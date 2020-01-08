FROM ruby:2.4.1-slim


RUN apt-get update \
    && apt-get install -y \
    git \
    curl \
    python-pip \
    python-dev

#Install nodejs
RUN echo 'Getting the NodeJS 6.x'

RUN curl -sL https://deb.nodesource.com/setup_6.x | bash -
RUN apt-get install -y \
    nodejs

RUN pip install awscli

RUN gem install jekyll bundler --no-rdoc --no-ri

RUN npm install -g yarn gulp \
    && rm -rf /var/cache/apk/*
