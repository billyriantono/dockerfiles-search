FROM alpine
MAINTAINER Sergey Z "sergey.zsw.w@gmail.com"

ENV CS_WORKDIR /var/www/html
ENV CS_RUBY_CFG $CS_WORKDIR/config.rb

RUN apk add --update \
        ruby \
        ruby-dev \
        libffi-dev \
        build-base \
        ruby-json \
        ruby-dev \
        ruby-irb \
        ruby-rdoc \

    && gem update --system \

    && gem install \
        listen \
        sass \
        compass \

    && apk del \
        build-base \
        libffi-dev \
        ruby-dev \

    && rm -rf /var/cache/apk/* \

    && mkdir -pv /var/www/html \

    && echo "sass_dir = '/var/www/html'" > $CS_RUBY_CFG \
    && echo >> $CS_RUBY_CFG

WORKDIR $CS_WORKDIR

VOLUME $CS_WORKDIR

ENTRYPOINT [ "compass" ]
