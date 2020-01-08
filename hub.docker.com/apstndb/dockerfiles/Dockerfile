FROM ruby:2.3-alpine

# python2 がないと node-gyp がエラー
# tzdata がないと rake db:migrate がエラー
# linux-headers は sys/types.h が必要なもののため
RUN apk --no-cache add bash gcc git g++ imagemagick-dev make musl-dev mysql-dev \
    nodejs python linux-headers tzdata
