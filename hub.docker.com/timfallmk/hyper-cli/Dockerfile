FROM ubuntu:latest
MAINTAINER "Tim <tim@vapor.io>"

ADD https://hyper-install.s3.amazonaws.com/hyper-linux-x86_64.tar.gz /tmp/
RUN tar xvf /tmp/hyper-linux-x86_64.tar.gz -C /usr/local/bin/
RUN chmod +x /usr/local/bin/hyper

ENTRYPOINT ["/usr/local/bin/hyper"]
