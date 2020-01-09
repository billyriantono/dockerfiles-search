# Version: 0.0.1
FROM ubuntu:18.04
MAINTAINER Richard Zhang "xyz0330@aliyun.com"
ENV REFRESHED_AT 2019-07-08
RUN apt-get -qq update
RUN apt-get install -y nginx

RUN mv /var/www/html/index.nginx-debian.html /var/www/html/bak.index.nginx-debian.html
ADD index.html /var/www/html/index.html
ADD SampleJunitResult.xml /var/www/html/SampleJunitResult.xml

VOLUME ["/opt/project"]
EXPOSE 80
#USER nginx
#ENTRYPOINT ["/usr/sbin/nginx"]
CMD ["/usr/sbin/nginx", "-g", "daemon off;"]
