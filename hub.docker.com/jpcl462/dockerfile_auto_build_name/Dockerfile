#Version 0.1
FROM ubuntu:latest
MAINTAINER workingwoki
RUN apt-get -yqq update && apt-get install -yqq apache2 && apt-get clean
CMD ["/usr/sbin/apache2ct1", "-D", "FOREGROUND"]
