FROM fauria/vsftpd
MAINTAINER zterry <zterry@qq.com>

RUN \
  rpm --rebuilddb && yum clean all && \
  yum install -y epel-release && \
  yum update -y && \
  yum remove -y httpd && \
  yum install -y \
                  supervisor \
                  nginx && \
  yum clean all

ADD run-nginx.sh /usr/sbin/run-nginx.sh
ADD nginx.conf /etc/nginx/nginx.conf
ADD vsftpd.conf /etc/vsftpd/
ADD supervisord.conf /etc/supervisord.conf
RUN chmod +x /usr/sbin/run-nginx.sh

CMD ["/usr/bin/supervisord", "-c", "/etc/supervisord.conf"]
