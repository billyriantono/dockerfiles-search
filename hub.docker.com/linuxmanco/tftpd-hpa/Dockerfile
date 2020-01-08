FROM ubuntu

RUN apt update
RUN apt install tftp-hpa tftpd-hpa -y

RUN mkdir /tftpboot
RUN chmod -R 777 /tftpboot

EXPOSE 69

CMD ["/usr/sbin/in.tftpd", "--foreground", "--listen", "-u", "root", "--secure", "--create", "/tftpboot"]