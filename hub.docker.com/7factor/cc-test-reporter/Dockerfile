FROM bash:5.0.2

ARG REPORTER_VERSION=0.6.4
RUN wget https://codeclimate.com/downloads/test-reporter/test-reporter-$REPORTER_VERSION-linux-amd64 -O /usr/bin/cc-test-reporter && chmod 755 /usr/bin/cc-test-reporter

RUN apk add --no-cache git