FROM alpine:3.8
MAINTAINER jarvan <valoran.jayce@gmail.com>
LABEL Description="vsftpd Docker image based on alpine:3.8"
ENV FTP_USER=admin \
    FTP_PASS=admin \
    PASV_ADDRESS=0.0.0.0 \
    PASV_MIN=21100 \
    PASV_MAX=21110

RUN apk update && apk upgrade && apk --update --no-cache add vsftpd &&  apk --update --no-cache add tzdata

RUN ln -sf /usr/share/zoneinfo/Asia/Shanghai /etc/localtime && echo "Asia/Shanghai" > /etc/timezone

RUN echo "local_enable=YES" >> /etc/vsftpd/vsftpd.conf \
  && echo "use_localtime=YES" >> /etc/vsftpd/vsftpd.conf \
  && echo "chroot_local_user=YES" >> /etc/vsftpd/vsftpd.conf \
  && echo "allow_writeable_chroot=YES" >> /etc/vsftpd/vsftpd.conf \
  && echo "background=NO" >> /etc/vsftpd/vsftpd.conf \
  && echo "ftpd_banner=Welcome to FTP Server" >> /etc/vsftpd/vsftpd.conf \
  && echo "dirmessage_enable=YES" >> /etc/vsftpd/vsftpd.conf \
  && echo "max_clients=10" >> /etc/vsftpd/vsftpd.conf \
  && echo "max_per_ip=5" >> /etc/vsftpd/vsftpd.conf \
  && echo "write_enable=YES" >> /etc/vsftpd/vsftpd.conf \
  && echo "local_umask=022" >> /etc/vsftpd/vsftpd.conf \
  && echo "passwd_chroot_enable=yes" >> /etc/vsftpd/vsftpd.conf \
  && echo "pasv_enable=Yes" >> /etc/vsftpd/vsftpd.conf \
  && echo "listen_ipv6=NO" >> /etc/vsftpd/vsftpd.conf \
  && echo "seccomp_sandbox=NO" >> /etc/vsftpd/vsftpd.conf \
  && sed -i "s/anonymous_enable=YES/anonymous_enable=NO/" /etc/vsftpd/vsftpd.conf

COPY vsftpd.sh /usr/sbin/

RUN chmod +x /usr/sbin/vsftpd.sh

EXPOSE 20 21 21100-21110

CMD /usr/sbin/vsftpd.sh

