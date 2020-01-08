FROM debian:jessie

RUN apt-get -y update
RUN apt-get -y install \
  build-essential \
  zlib1g-dev \
  ruby \
  ruby-dev

RUN gem install \
  github-pages

EXPOSE 4000

WORKDIR /code

ENTRYPOINT ["jekyll"]
