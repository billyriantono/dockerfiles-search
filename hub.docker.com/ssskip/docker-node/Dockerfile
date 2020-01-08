FROM node:10-alpine

RUN apk add --no-cache \
        coreutils \
        python \
        git \
        make \
        gcc \
        g++ \
        sudo \
        ruby \
        ruby-dev \
        openssl-dev \
        linux-headers \
        py-pip 
        
RUN pip install --upgrade pip && pip install s3cmd && pip install awscli --upgrade

RUN npm install -g jsonlint-cli

RUN gem install compass --no-document
