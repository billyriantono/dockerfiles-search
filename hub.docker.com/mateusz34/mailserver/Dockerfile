FROM debian:9.9


ENV DEBIAN_FRONTEND noninteractive

RUN apt update 
RUN apt-get install -y gnupg2 lsb-release wget
RUN wget -O- https://rspamd.com/apt-stable/gpg.key | apt-key add -
RUN echo "deb http://rspamd.com/apt-stable/ $(lsb_release -c -s) main" > /etc/apt/sources.list.d/rspamd.list
RUN echo "deb-src http://rspamd.com/apt-stable/ $(lsb_release -c -s) main" >> /etc/apt/sources.list.d/rspamd.list
RUN apt update
RUN apt install fail2ban procps redis-server rspamd dovecot-core dovecot-imapd dovecot-lmtpd dovecot-mysql dovecot-sieve dovecot-managesieved dovecot-pop3d postfix rsyslog supervisor -y

ADD assets/install.sh /install.sh
RUN chmod 700 /install.sh

ADD assets/smtp /smtp

ADD assets/service.sh /service.sh
RUN chmod 700 /service.sh

ADD assets/rspamd.sh /rspamd.sh
RUN chmod 700 /rspamd.sh

ADD assets/postmap.sh /postmap.sh
RUN chmod 700 /postmap.sh

ADD assets/dkim.sh /dkim.sh
RUN chmod 700 /dkim.sh

RUN rm /etc/dovecot/dovecot.conf && rm /etc/postfix/main.cf && rm /etc/postfix/master.cf
ADD assets/dovecot.conf /etc/dovecot/dovecot.conf
ADD assets/main.cf /etc/postfix/main.cf
ADD assets/master.cf /etc/postfix/master.cf
ADD assets/rspamd/local.d/* /etc/rspamd/local.d/

CMD /install.sh
