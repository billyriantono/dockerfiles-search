FROM alpine:latest

RUN sed -i -e 's/v3\.7/edge/g' /etc/apk/repositories && \
      apk add --no-cache curl git build-base libffi-dev cmake tzdata \
      ruby ruby-dev ruby-bundler ruby-etc ruby-json ruby-irb ruby-bigdecimal libxml2-dev \
      imagemagick nodejs nodejs-npm yarn postgresql postgresql-libs postgresql-dev

