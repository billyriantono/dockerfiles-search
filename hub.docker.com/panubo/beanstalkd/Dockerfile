FROM debian:latest

RUN apt-get update && \
    apt-get -y install beanstalkd && \
    apt-get -y clean && \
    rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

EXPOSE 11300

CMD ["/usr/bin/beanstalkd", "-u", "nobody"]

