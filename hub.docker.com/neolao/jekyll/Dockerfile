FROM ruby:2.1
MAINTAINER contact@neolao.com

RUN set -e; \
    apt-get update; \
    apt-get install -y node python-pygments; \
    apt-get clean; \
    rm -rf /var/lib/apt/lists/*

RUN gem install \
   github-pages \
   jekyll \
   jekyll-redirect-from \
   execjs \
   therubyracer

VOLUME /source

WORKDIR /source
ENTRYPOINT ["jekyll"]
