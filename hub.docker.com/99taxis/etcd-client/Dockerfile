FROM ruby:2.3.1-alpine
MAINTAINER "Fabio Hisamoto" <fabio@99taxis.com>

RUN apk add --no-cache curl bash sudo

# install etcdctl
RUN curl -sSL -o /usr/local/bin/etcdctl https://s3-us-west-2.amazonaws.com/get-deis/etcdctl-v0.4.9 \
    && chmod +x /usr/local/bin/etcdctl

RUN gem install etcd
