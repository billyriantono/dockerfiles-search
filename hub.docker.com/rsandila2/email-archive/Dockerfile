FROM centos:7
VOLUME /dovecot_mail
EXPOSE 143
RUN /usr/bin/yum upgrade -y
RUN /usr/bin/yum -y install dovecot dovecot-pigeonhole rsyslog
COPY key.pem /etc/dovecot/key.pem
COPY cert.pem /etc/dovecot/cert.pem
COPY dovecot.conf /etc/dovecot/dovecot.conf
COPY rsyslog.conf /etc/rsyslog.conf
COPY startup.sh /startup.sh
CMD /startup.sh
