FROM ruby:latest
LABEL maintainer "Michael Henke <433270+aphex3k@users.noreply.github.com>"
RUN gem install travis

RUN mkdir -p /usr/local/bin
RUN mkdir -p /data

WORKDIR /data/

COPY travis-lint.sh /usr/local/bin/
COPY .travis.yml /data/.travis.yml

RUN travis lint .travis.yml && rm .travis.yml

ENTRYPOINT ["bash", "/usr/local/bin/travis-lint.sh"]