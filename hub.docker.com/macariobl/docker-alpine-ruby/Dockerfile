FROM alpine:latest

ENV PATH /root/.gem/ruby/2.3.0/bin:$PATH

RUN apk add --no-cache git build-base libffi-dev cmake tzdata \
      ruby ruby-dev ruby-bundler ruby-irb ruby-bigdecimal \
      imagemagick nodejs postgresql postgresql-libs \
      postgresql-dev openssh-client linux-headers zlib-dev \
      python
