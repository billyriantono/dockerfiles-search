FROM debian:latest
MAINTAINER Al West

RUN apt-get update && apt-get install -y collectd
ADD collectd.conf /etc/collectd/
ADD entrypoint.sh /entrypoint.sh
RUN chmod +x /entrypoint.sh

ENTRYPOINT ["/entrypoint.sh"]
