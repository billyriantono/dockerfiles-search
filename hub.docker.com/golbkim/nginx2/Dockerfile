#Dockerfile - Nginx
FROM ubuntu:16.04
MAINTAINER dohyoung kim(golbkim@daum.net)

##RUN echo "nameserver 8.8.8.8 > /etc/resolv.conf" 

RUN sed -i 's/archive.ubuntu.com/ftp.daumkakao.com/g' /etc/apt/sources.list
RUN apt-get update && apt-get install -y supervisor nginx
RUN mkdir -p /var/log/supervisor
ADD supervisord.conf /etc/supervisor/conf.d/supervisord.conf
EXPOSE 80
CMD ["/usr/bin/supervisord"]






