FROM golang:latest

MAINTAINER Minh-Quan TRAN "account@itscaro.me"

RUN apt-get update && \
	apt-get install -y wget

RUN apt-get update && \
	apt-get install -y \
		openssh-server supervisor curl git nano && \
    rm -rf /var/lib/apt/lists/* && \
	apt-get clean

RUN echo 'root:root' |chpasswd

RUN sed -ri 's/^PermitRootLogin\s+.*/PermitRootLogin yes/' /etc/ssh/sshd_config && \
	sed -ri 's/UsePAM yes/#UsePAM yes/g' /etc/ssh/sshd_config

RUN mkdir -p /var/run/sshd

ADD supervisord.conf /etc/supervisor/conf.d/supervisord.conf
ADD start.sh /start.sh

VOLUME ["/go", "/root"]

EXPOSE 22 80 443 1080 8080

ENTRYPOINT ["/start.sh"]

#CMD [""]