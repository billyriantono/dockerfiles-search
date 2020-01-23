FROM ubuntu:16.04

RUN apt-get update \
    && apt-get install -y  vsftpd \
    && apt-get install -y db-util \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/*


ENV FTP_USER=$FTP_USER \
    FTP_PASS=$FTP_PASS \
    PASV_ADDRESS=$PASC_ADDRESS \
    PASV_MIN_PORT=$PASV_MIN_PORT \
    PASV_MAX_PORT=$PASV_MAX_PORT


COPY vsftpd.conf /etc/
COPY vsftpd_virtual /etc/pam.d/
COPY start_vsftpd /start_vsftpd

RUN chmod +x /start_vsftpd \
    && mkdir -p /var/vsftpd/ \
    && chown -R ftp:ftp /var/vsftpd/ \
    && mkdir -p var/run/vsftpd/empty

VOLUME /var/vsftpd
VOLUME /var/log/vsftpd

#EXPOSE 20-21
#EXPOSE $PASV_MIN_PORT-$PASV_MAX_PORT

ENTRYPOINT ["/start_vsftpd"]
