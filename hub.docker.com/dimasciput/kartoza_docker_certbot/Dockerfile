FROM library/ubuntu:16.04
MAINTAINER Dimas Ciputra<dimas@kartoza.com>

RUN apt-get update -y && \
	apt-get install -y software-properties-common && \ 
	add-apt-repository ppa:certbot/certbot && \ 
	apt-get update -y && \ 
	apt-get install -y python-certbot-nginx

WORKDIR /

COPY generate_certificate.sh /generate_certificate.sh
RUN chmod +x /generate_certificate.sh

ENTRYPOINT [ "./generate_certificate.sh" ]
