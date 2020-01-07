FROM riet/sshd
MAINTAINER riet
RUN yum install -y nginx
EXPOSE 80
EXPOSE 443
ADD run.sh /usr/local/sbin/run.sh
RUN chmod +x /usr/local/sbin/run.sh
CMD  ["/usr/local/sbin/run.sh"]
