FROM ruby:alpine

RUN apk add --no-cache \
        build-base \
        make && \
    gem install bundler

EXPOSE 4000 

ENTRYPOINT [ "bundle" ]

CMD [ "exec", "jekyll", "serve", "-H", "0.0.0.0", "--force_polling" ]
