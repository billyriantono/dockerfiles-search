FROM ubuntu:latest
MAINTAINER d.basivireddy@gmail.com
RUN apt-get update && apt-get install -y memcached supervisor
COPY supervisord.conf /etc/supervisor/conf.d/supervisord.conf
EXPOSE 11211
CMD ["/usr/bin/supervisord"]
