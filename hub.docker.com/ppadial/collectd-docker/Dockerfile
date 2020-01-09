FROM ubuntu:trusty
MAINTAINER Paulino Padial <github.com/ppadial>

RUN apt-get update && \
    apt-get upgrade -y && \
    apt-get install -y collectd collectd-utils

COPY ./run.sh /run.sh
RUN chmod +x /run.sh

VOLUME ["/etc/collectd"]

CMD ["/run.sh"]

