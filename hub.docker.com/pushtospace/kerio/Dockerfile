FROM ubuntu:14.04

MAINTAINER Gino Jongenelen <g.jongenelen@pushto.space>

RUN apt-get update && apt-get install lsof sysstat wget -y

RUN wget -O kerio-connect-linux-64bit.deb http://download.kerio.com/dwn/kerio-connect-linux-64bit.deb
RUN dpkg -i kerio-connect-linux-64bit.deb

RUN locale-gen en_US.utf8

EXPOSE 4040 25 465 587 110 995 143 993 119 563 389 636 80 443 5222 5223

COPY start.sh /start.sh
RUN chmod +x /start.sh

CMD ["/start.sh"]