FROM ghost:0.6.4
MAINTAINER j.ciolek@webnicer.com
RUN apt-get update && apt-get install -y supervisor
RUN mkdir -p /var/log/supervisor
COPY supervisor/* /etc/supervisor/conf.d/
CMD ["/usr/bin/supervisord"]
