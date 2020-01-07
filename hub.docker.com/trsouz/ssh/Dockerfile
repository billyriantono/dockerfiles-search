FROM debian:wheezy
MAINTAINER Thiago Rodrigues <thiagorsouz@gmail.com>
RUN apt-get update -qq \
    && apt-get install -y -qq \
    ssh \
    && rm -rf /var/lib/apt/lists/* \
    && apt-get autoremove

ADD ssh /usr/local/bin/ssh
RUN chmod +x /usr/local/bin/ssh && mkdir -p /root/.ssh
ENTRYPOINT ["/usr/local/bin/ssh"]
CMD []
