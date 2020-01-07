FROM ubuntu:trusty
COPY nginx.list /etc/apt/sources.list.d/nginx.list
COPY nginx_signing.key /tmp/nginx_signing.key
RUN \
	apt-key add /tmp/nginx_signing.key && \
	rm /tmp/nginx_signing.key && \
	apt-get update && \
	apt-get install -y nginx


