FROM debian:latest
MAINTAINER Carlos Meza <carlos@droots.org>
ENV DEBIAN_FRONTEND noninteractive
RUN apt-get update
RUN apt-get upgrade -y
RUN apt-get install -y vim
RUN apt-get clean
ADD run.sh /run.sh
RUN chmod +x /run.sh
CMD ["/run.sh"]
