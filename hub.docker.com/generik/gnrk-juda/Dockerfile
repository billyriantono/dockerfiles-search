FROM ruby:alpine
LABEL author="GNRK"
LABEL license="MIT"
LABEL traefik.backend.healthcheck.path="/"

ADD . /app

WORKDIR /app
RUN bundle

EXPOSE 9292

CMD rackup -E production
