FROM ruby:2.4.0-alpine
#MAINTAINER Tobias Gesellchen <tobias@gesellix.de> (@gesellix)

RUN apk add --no-cache git \
    && apk add --no-cache --virtual build-deps build-base \
    && gem install travis \
    && apk del build-deps
WORKDIR /proj

ENTRYPOINT ["travis"]
CMD ["help"]
