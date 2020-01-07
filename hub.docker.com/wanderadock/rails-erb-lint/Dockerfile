FROM alpine:3.6
RUN apk --no-cache --update add ruby
RUN apk --no-cache --update add build-base ruby-dev zlib-dev && \
    gem install rails-erb-lint --no-document && \
    apk del build-base ruby-dev zlib-dev && \
    rm -rf /var/cache/apk/*
WORKDIR /lint
ENTRYPOINT ["rails-erb-lint"]
