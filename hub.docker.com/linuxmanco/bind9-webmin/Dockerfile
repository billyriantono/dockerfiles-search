FROM ubuntu

RUN rm /etc/apt/apt.conf.d/docker-gzip-indexes
RUN apt update
RUN apt install libnet-ssleay-perl libauthen-pam-perl libio-pty-perl apt-show-versions perl wget python bind9 -y

RUN wget https://prdownloads.sourceforge.net/webadmin/webmin_1.890_all.deb
RUN dpkg -i webmin_1.890_all.deb

RUN echo 'root:root' | chpasswd
RUN cp /etc/webmin/webmin.acl /etc/webmin/webmin.acl.bak
RUN echo root: backup-config bind8 passwd system-status webmin webmincron webminlog time > /etc/webmin/webmin.acl

ADD startup.sh /usr/bin/startup.sh

EXPOSE 10000
EXPOSE 53

CMD ["/bin/sh", "/usr/bin/startup.sh"]