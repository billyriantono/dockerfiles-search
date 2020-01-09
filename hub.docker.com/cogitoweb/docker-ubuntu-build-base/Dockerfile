FROM ubuntu:18.04

RUN apt-get update && \
	apt-get install -y ssh rsync wget git python-pip openvpn && \
	(rm -f /var/cache/apt/archives/*.deb \
	      /var/cache/apt/archives/partial/*.deb \
	      /var/cache/apt/*.bin || \
	true)
RUN pip install --upgrade google-api-python-client 