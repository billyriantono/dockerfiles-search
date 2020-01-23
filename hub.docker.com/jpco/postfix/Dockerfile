FROM resin/armv7hf-debian-qemu

#
# Set map these files:
#  /var/mail/virtual_aliases
#  /var/mail/virtual_mailbox_domains

# Set Environment
ENV \
 DEBIAN_FRONTEND=noninteractive \
 MAIL_DOMAIN=example.com \
 POSTFIX_HOSTNAME=smtp.example.com \
 POSTFIX_SSL_CERT_PATH=/etc/ssl/certs/ssl-cert-snakeoil.pem \
 POSTFIX_SSL_CERT_KEY=/etc/ssl/private/ssl-cert-snakeoil.key \
 SASL_HOST=dovecot \
 SASL_PORT=12345 \
 LMTP_HOST=dovecot \
 LMTP_PORT=24 \
 SPAMASSASSIN=false

COPY assets/bin/ /bin/ 

# Start editing 
# Install package here for cache 
# Postfix install workaround for crosscompiler
# Backup overrides
RUN ["cross-build-start"]
RUN \
  apt-get update && \
  apt-get download postfix && \
  dpkg --unpack postfix*.deb && \
  rm postfix_* && \
  dpkg-divert --add --rename --divert /usr/local/bin/newaliases /bin/true  && \
  apt-get -fy install && \
  dpkg-divert --remove --rename /usr/bin/newaliases && \
  apt-get -y install rsyslog \
  spamassassin spamc && \
  cp -b /etc/postfix/main.cf /etc/postfix/main.cf.bak && \
  cp -b /etc/postfix/master.cf /etc/postfix/master.cf.bak && \
  chmod a+x bin/*.sh && \
  touch /var/mail/virtual_aliases && \
  touch /var/mail/virtual_mailbox_domains && \
  sed -i 's/CRON=0/CRON=1/g; s/ENABLED=0/ENABLED=1/g' /etc/default/spamassassin \
  && sed -i 's/# rewrite_header/rewrite_header/g; s/# required_score/required_score/g; s/# use_bayes/use_bayes/g; s/# bayes_auto_learn/bayes_auto_learn/g; s/\*SPAM\*/\* SPAM _SCORE_ \*/g'  /etc/spamassassin/local.cf && \
  apt-get clean && \
  rm -rf /var/lib/apt/lists/* \
  	/tmp/* \
  	/var/tmp/*
RUN ["cross-build-end"]

#Copy asset
COPY assets/etc/postfix /etc/postfix/

ENTRYPOINT ["entrypoint.sh"]
CMD ["tail", "-n", "1", "-F", "/var/log/syslog"]
