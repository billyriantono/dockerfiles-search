FROM kalilinux/kali-rolling
MAINTAINER chasepd <1214246+chasepd@users.noreply.github.com>

#environment-variables for non-interactive shell:
ENV DEBIAN_FRONTEND noninteractive

#install updates and the sqlmap package:
RUN apt-get update \
  && apt-get upgrade -y\
  && apt-get -y install sqlmap 

ENTRYPOINT ["/usr/bin/sqlmap"]
