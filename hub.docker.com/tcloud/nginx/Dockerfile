# tcloud/nginx
# VERSION        0.1

FROM tcloud/base
MAINTAINER tcloud

USER root

RUN yum -y install nginx && \
	yum clean all && \
	mkdir -p /var/lib/nginx/tmp

WORKDIR /data

VOLUME ["/var/lib/nginx","/etc/nginx","/log","/data"]

EXPOSE 80 443

# We use the "sh -c" to turn around https://github.com/docker/docker/issues/5509 - variable not expanded
ENTRYPOINT ["sh", "-c"]

CMD ["nginx"]