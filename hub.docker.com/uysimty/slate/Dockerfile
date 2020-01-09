FROM ruby:2.5-alpine
EXPOSE 4567

RUN apk update \
 && apk add coreutils git make g++ nodejs

RUN git clone --branch v2.3.1 https://github.com/lord/slate /slate

RUN cd /slate && bundle install

VOLUME /slate/source
VOLUME /slate/build

CMD cd /slate && exec bundle exec middleman server --watcher-force-polling
