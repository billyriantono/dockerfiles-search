# 此处必须使用3.7版本
FROM alpine:3.7
MAINTAINER Lei Zhang <coolbeevip@gmail.com>

# Install and configure Apache WebDAV and Subversion
RUN apk --no-cache add apache2 apache2-utils apache2-webdav mod_dav_svn subversion
ADD vh-davsvn.conf /etc/apache2/conf.d/
RUN mkdir -p /run/apache2

ADD run.sh /
ADD authz /tmp
RUN chmod +x /run.sh
ADD httpd.conf /etc/apache2
EXPOSE 80

# Define default command
CMD ["/run.sh"]
