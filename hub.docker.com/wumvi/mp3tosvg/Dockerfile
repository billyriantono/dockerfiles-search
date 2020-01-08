FROM php:7.2.1-cli-stretch
MAINTAINER Vitaliy Kozlenko <vk@wumvi.com>

LABEL version="0.0.2"

RUN DEBIAN_FRONTEND=noninteractive && \
    apt-get update && \
    apt-get --no-install-recommends -qq -y install sox -y && \
	# apt-get remove -y   && \
	apt-get autoremove -y && \
	rm -rf /soft/ && \
	rm -rf /var/lib/apt/lists/* && \
	echo 'end'

WORKDIR /code/
