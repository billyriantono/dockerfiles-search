FROM ruby:2.3.3-alpine

ENV BUILD_PACKAGES="curl-dev build-base openssh" \
    DEV_PACKAGES="tzdata libxml2 libxml2-dev libxslt libxslt-dev mysql-client \
      qt5-qtwebkit qt-dev bash curl imagemagick imagemagick-dev mysql-dev \
      openssl-dev sqlite-dev git gcc g++ make nodejs vim postgresql-dev"

RUN apk --update --upgrade add $BUILD_PACKAGES $DEV_PACKAGES
RUN rm /var/cache/apk/*
RUN curl -Ls https://github.com/arobson/docker-phantomjs2/releases/download/v2.1.1-20160523/dockerized-phantomjs.tar.gz \
       | tar xz -C /

CMD ["bash"]
