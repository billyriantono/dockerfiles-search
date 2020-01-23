FROM eiel/gentoo
MAINTAINER Tomohiko Himura <eiel.hal@gmail.com>

WORKDIR /usr
ADD install-portage.sh .
RUN sh /install-portage.sh
RUN emerge banner 
CMD banner docker
