# Set the base image to CentOS 7
FROM centos:7

# File Author / Maintainer
MAINTAINER Marc-Jan Barnhoorn

RUN useradd -ms /bin/bash www && \
    yum -y makecache fast && \
    yum -y update && \
    yum -y install epel-release && \
    yum -y install httpd mod_ssl && \
    yum -y clean all && \
    rm -fr /tmp/* /var/tmp/* /var/cache/yum && \
    rm /etc/httpd/conf.d/welcome.conf && \
    sed -i -e "s/\/var\/www\/html/\/var\/www/g" /etc/httpd/conf/httpd.conf && \
    sed -i -e "s/User apache/User www/g" /etc/httpd/conf/httpd.conf && \
    sed -i -e "s/Group apache/Group www/g" /etc/httpd/conf/httpd.conf

# Adding the Vhosts
ADD virtualhosts.conf /etc/httpd/conf.d/virtualhosts.conf

# Adding SSL certificates
ADD ssl /etc/letsencrypt

ENV TERM xterm

# Set the port to 80 and 443
EXPOSE 80 443

COPY docker-entrypoint.sh /

ENTRYPOINT ["/docker-entrypoint.sh"]
