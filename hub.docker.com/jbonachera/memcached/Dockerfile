FROM fedora:23
MAINTAINER Julien BONACHERA <julien@bonachera.fr>
RUN dnf install -y memcached
EXPOSE 11211
USER memcached
CMD ["/usr/bin/memcached", "-l", "0.0.0.0"]
