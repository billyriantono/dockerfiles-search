FROM centos:7
MAINTAINER Gustavo J Gallardo <ggallard@identicum.com>

RUN yum -y update && \
    yum -y install httpd wget

RUN ln -sf /dev/stdout /var/log/httpd/access_log && \
    ln -sf /dev/stderr /var/log/httpd/error_log

RUN rm -f /etc/httpd/conf.d/userdir.conf && \
    rm -f /etc/httpd/conf.d/welcome.conf

EXPOSE 80

# Simple startup script to avoid some issues observed with container restart
ADD run-httpd.sh /run-httpd.sh
RUN chmod -v +x /run-httpd.sh

CMD ["/run-httpd.sh"]
