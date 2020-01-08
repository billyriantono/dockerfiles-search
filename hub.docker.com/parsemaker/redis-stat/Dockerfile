FROM ruby:2.4

LABEL maintainer="hgati <cobays@gmail.com>"

RUN gem install redis-stat

EXPOSE 63790

ENTRYPOINT ["redis-stat"]