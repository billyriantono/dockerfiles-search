FROM ruby:2.6.3-alpine

RUN apk update \
  && apk add --update-cache libffi-dev \
                            readline \
                            build-base \
                            mysql-client \
                            mysql-dev \
                            libc-dev \
                            linux-headers \
                            libxml2-dev \
                            libxslt-dev \
                            readline-dev \
                            gcc \
                            libc-dev \
  && rm -rf /var/cache/apk/*

CMD [ "irb" ]
