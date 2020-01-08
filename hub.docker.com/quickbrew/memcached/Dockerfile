FROM ubuntu:latest
MAINTAINER Simon Menke <simon.menke@gmail.com>

RUN apt-get update
RUN apt-get -y install memcached

EXPOSE 11211
USER   nobody

CMD ["-m", "128"]
ENTRYPOINT ["memcached", "-p", "11211", "-U", "0"]
