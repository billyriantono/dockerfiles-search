FROM ubuntu:14.04

RUN apt-get update
RUN apt-get upgrade -y
RUN apt-get install -y bind9

ADD ./etc/bind /etc/bind
ADD start-tsh-dns /start-tsh-dns

EXPOSE 53

CMD ["/start-tsh-dns"]