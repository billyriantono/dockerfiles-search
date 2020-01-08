FROM node:8.15-alpine

RUN apk -v --update add \
        curl \
        lcms2-dev \
        git \
        bash \
        python \
        py-pip \
        groff \
        less \
        mailcap \
        make \
        gcc \
        g++ \
        autoconf \
        automake \
        libpng-dev \
        && \
    pip install --upgrade awscli==1.14.5 s3cmd==2.0.1 python-magic && \
    git clone https://github.com/tfutils/tfenv.git ~/.tfenv && \
    ln -s ~/.tfenv/bin/* /usr/local/bin && \
    tfenv install 0.12.13 && \
    terraform -v && \
    apk -v --purge del py-pip && \
    rm /var/cache/apk/*

