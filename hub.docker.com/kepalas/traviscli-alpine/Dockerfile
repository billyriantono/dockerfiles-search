FROM ruby:2.6.3-alpine3.9

LABEL maintainer="Tadas Kepalas <tadas@kepalas.lt>"

RUN apk add --no-cache --update-cache bash coreutils build-base  \
    && gem install travis \
    && apk del --purge build-base

CMD ["/bin/bash"]
