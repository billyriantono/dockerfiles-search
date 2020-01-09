FROM ubuntu:latest

ENV DEBIAN_FRONTEND noninteractive
# run
RUN apt-get -y update && apt-get clean all
RUN apt-get install -y \
	vsftpd \
	&& apt-get clean all

COPY vsftpd /etc/pam.d/
COPY vsftpd-config.sh /etc/vsftpd/

RUN chmod +x /etc/vsftpd/vsftpd-config.sh
RUN mkdir -p /data/ftp/
RUN chown -R ftp:ftp /data/ftp/

VOLUME [ "/data/ftp" ]
VOLUME [ "/var/log/vsftpd" ]

EXPOSE 21 20

ENTRYPOINT ["/etc/vsftpd/vsftpd-config.sh"]

CMD ["/usr/sbin/vsftpd /etc/vsftpd/vsftpd.conf"]
