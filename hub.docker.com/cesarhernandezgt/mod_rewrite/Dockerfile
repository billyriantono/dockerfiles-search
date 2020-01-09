FROM centos:7

RUN yum -y --setopt=tsflags=nodocs update && \
    yum -y --setopt=tsflags=nodocs install httpd && \
    yum clean all

# Enable the .htaccess functionality on httpd
RUN sed -i 's/AllowOverride[[:space:]]None/AllowOverride All/' /etc/httpd/conf/httpd.conf
EXPOSE 80

# Simple startup script to avoid some issues observed with container restart
ADD run-httpd.sh /run-httpd.sh
RUN chmod -v +x /run-httpd.sh

CMD ["/run-httpd.sh"]
