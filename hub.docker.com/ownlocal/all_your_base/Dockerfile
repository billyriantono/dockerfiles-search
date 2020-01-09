FROM alpine:3.3

RUN apk update && apk upgrade && \
    apk add ruby ruby-dev ruby-irb ruby-io-console ruby-rake ruby-bigdecimal ruby-minitest ruby-json && \
    apk add ca-certificates && \
    gem install --no-ri --no-doc bundler && \
    bundle config --global silence_root_warning 1 && \
    bundle config --global build.nokogiri --use-system-libraries && \
    bundle config --global build.therubyracer --use-system-libraries && \
    rm -f /var/cache/apk/* /usr/lib/ruby/gems/2.2.0/cache/*
