FROM ubuntu:14.04
MAINTAINER Artem Berdyshev "a.berdyshev@amgrade.com"


ENV DEBIAN_FRONTEND noninteractive

# Set timezone and locale.
RUN locale-gen en_US.UTF-8
ENV LANG en_US.UTF-8
ENV LANGUAGE en_US:en
ENV LC_ALL en_US.UTF-8


# Update the package repository
RUN apt-get update && \
    apt-get upgrade -y && \
    apt-get install -y memcached


EXPOSE 11211
USER daemon
ENTRYPOINT ["memcached", "-vv"]

CMD ["-m 256","-p 11211","-c 1024"]