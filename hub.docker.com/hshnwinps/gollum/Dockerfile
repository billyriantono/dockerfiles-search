FROM ruby:alpine3.7

RUN set -ex \
 && apk update \
 && apk add --no-cache --virtual .devdeps build-base icu-dev cmake \
 && apk add --no-cache icu-libs git \
 && gem install gollum github-markdown \
 && apk del .devdeps

WORKDIR /wiki

ENTRYPOINT ["gollum", "--port", "80", "--css", "--js", "--emoji", "--live-preview", "--show-all"]
EXPOSE 80
