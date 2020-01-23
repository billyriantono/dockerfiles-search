FROM ubuntu:16.04
MAINTAINER dewist s.r.o. dewist@dewist.com

WORKDIR /data
RUN apt-get update && apt-get install -yy --no-install-recommends \
	python \
	python-pip \ 
	python-dev \
	python-wheel \
	python-setuptools \
    ssh \
	vim \
	gcc \
	curl \
	zip \
	unzip \
	&& pip install \
	boto \
	boto3 \
	awscli \
	ansible==2.4.1.0 \
	&& apt-get clean
RUN curl -o /tmp/terraform.zip https://releases.hashicorp.com/terraform/0.11.3/terraform_0.11.3_linux_amd64.zip
RUN unzip /tmp/terraform.zip -d /usr/local/bin/
RUN chmod +x /usr/local/bin/terraform
COPY ansible.cfg /root/.ansible.cfg
