# How-To
 # Local Build: docker build -t nginx .
 # Local Run: docker run -it --rm nginx

FROM centos:7.5.1804
MAINTAINER Duan Li <inputx@goodays.com>


RUN yum --enablerepo=extras install epel-release -y && \
	yum install unzip git nginx openssl -y && \
	yum clean all &&\
	rm -rf /var/cache/yum

EXPOSE 80 8000 8080 8008 8800 443

user nginx

# ENTRYPOINT ["entrypoint"]
# CMD [ "nginx-1.12" ]