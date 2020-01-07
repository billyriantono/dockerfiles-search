FROM alpine:3.3

MAINTAINER Flug <flugv1@gmail.com>

# Skip installing gem documentation
RUN echo 'gem: --no-rdoc --no-ri' >> "$HOME/.gemrc"

RUN apk add --update --no-cache git build-base ruby-dev libffi-dev ruby-bundler ca-certificates && \
    gem install travis && \
    rm /var/cache/apk/* && \
    rm -rf /usr/share/ri

ENTRYPOINT ["/usr/bin/travis"]
