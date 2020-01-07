FROM ruby:stretch
MAINTAINER db@dotcore.net

RUN gem install  \
  jekyll \
  jekyll-paginate \
  kramdown \
  exifr \
  rmagick

VOLUME /src
EXPOSE 4000

WORKDIR /src
ENTRYPOINT ["jekyll"]
