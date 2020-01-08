FROM 1000kit/base

MAINTAINER 1000kit <docker@1000kit.org>

LABEL org.1000kit.vendor="1000kit" \
      org.1000kit.license=GPLv3 \
      org.1000kit.version=1.0.0
  
USER root
  
ADD run-httpd.sh /root/run-httpd.sh  
# Install packages necessary to run apache
RUN  yum update -y \
   && yum -y install httpd \
   && yum clean all \
   && chmod -v +x /root/run-httpd.sh \
   && mkdir /var/www/html/Downloads   


EXPOSE 80

VOLUME /var/www/html

CMD ["/root/run-httpd.sh"]
      
#END