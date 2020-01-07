FROM fredericomartini/debian:8.4
MAINTAINER Frederico Martini <fredmalmeida@gmail.com>

# Let the conatiner know that there is no tty
ENV DEBIAN_FRONTEND noninteractive

COPY apache2/ /tmp/
ADD apache.sh /usr/sbin/ 
RUN chmod +x /usr/sbin/apache.sh
RUN sh /usr/sbin/apache.sh
EXPOSE 80

#clear cache
RUN apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

