FROM alpine:latest

MAINTAINER Jos Kore Wingfield

ENV VSFTP_USER UNSET
ENV VSFTP_PASS UNSET
ENV VSFTP_PASV_ADDR UNSET
ENV VSFTP_PASV_PORT_START 21100
ENV VSFTP_PASV_PORT_END 21110
ENV VSFTP_LOG true

RUN \
  apk add --no-cache \
    vsftpd openssl build-base linux-pam-dev curl tar

RUN \
  echo "listen=YES" > /etc/vsftpd/vsftpd.conf \
  && echo "background=NO" >> /etc/vsftpd/vsftpd.conf \
  && echo "anonymous_enable=NO" >> /etc/vsftpd/vsftpd.conf \
  && echo "write_enable=YES" >> /etc/vsftpd/vsftpd.conf \
  && echo "local_enable=YES" >> /etc/vsftpd/vsftpd.conf \
  && echo "guest_enable=YES" >> /etc/vsftpd/vsftpd.conf \
  && echo "virtual_use_local_privs=YES" >> /etc/vsftpd/vsftpd.conf \
  && echo "user_sub_token=\$USER" >> /etc/vsftpd/vsftpd.conf \
  && echo "local_root=/home/vsftpd/\$USER" >> /etc/vsftpd/vsftpd.conf \
  && echo "chroot_local_user=YES" >> /etc/vsftpd/vsftpd.conf \
  && echo "allow_writeable_chroot=YES" >> /etc/vsftpd/vsftpd.conf \
  && echo "local_umask=022" >> /etc/vsftpd/vsftpd.conf \
  && echo "passwd_chroot_enable=YES" >> /etc/vsftpd/vsftpd.conf \
  && echo "seccomp_sandbox=NO" >> /etc/vsftpd/vsftpd.conf \
  && echo "pam_service_name=vsftpd_users" >> /etc/vsftpd/vsftpd.conf \
  && echo "pasv_enable=YES" >> /etc/vsftpd/vsftpd.conf \
  && echo "pasv_promiscuous=YES" >> /etc/vsftpd/vsftpd.conf \
  && echo "pasv_addr_resolve=NO" >> /etc/vsftpd/vsftpd.conf \
  && echo "port_enable=YES" >> /etc/vsftpd/vsftpd.conf \
  && echo "connect_from_port_20=YES" >> /etc/vsftpd/vsftpd.conf \
  && echo "ftp_data_port=20" >> /etc/vsftpd/vsftpd.conf \
  && echo "xferlog_enable=YES" >> /etc/vsftpd/vsftpd.conf \
  && echo "xferlog_file=/var/log/vsftpd/vsftpd.log" >> /etc/vsftpd/vsftpd.conf

RUN \
  echo "#%PAM-1.0" >> /etc/pam.d/vsftpd_users \
  && echo "auth     required  pam_pwdfile.so  pwdfile=/etc/vsftpd/vsftpd_users" >> /etc/pam.d/vsftpd_users \
  && echo "account	required	pam_permit.so" >> /etc/pam.d/vsftpd_users

RUN \
  mkdir /libpam \
  && cd /libpam \
  && curl -sSL https://github.com/tiwe-de/libpam-pwdfile/archive/v1.0.tar.gz | tar xz --strip 1 \
  && make install \
  && cd .. \
  && rm -rvf /libpam

COPY init-vsftpd.sh /usr/sbin/
RUN chmod +x /usr/sbin/init-vsftpd.sh
RUN mkdir -p /home/vsftpd/
RUN chown -R ftp:ftp /home/vsftpd/

RUN \
  apk del \
    build-base linux-pam-dev curl tar

VOLUME /home/vsftpd/
VOLUME /var/log/vsftpd

EXPOSE 20 21

CMD ["/usr/sbin/init-vsftpd.sh"]
