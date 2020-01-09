From ubuntu:trusty

# Set noninteractive mode for apt-get
ENV DEBIAN_FRONTEND noninteractive

# update & install
RUN apt-get update
RUN apt-get -y install supervisor postfix dovecot-common dovecot-imapd dovecot-pop3d whois

# Add files
ADD install.sh /
ADD create_user.sh /usr/local/bin/
ADD dovecot/10-auth.conf /etc/dovecot/conf.d/
ADD dovecot/10-master.conf /etc/dovecot/conf.d/
ADD postfix/master.cf /etc/postfix/
RUN chmod +x /install.sh /usr/local/bin/create_user.sh

# expose port
EXPOSE 25 110 143

# data volume directories
VOLUME ["/var/mail","/home"]

# Run
CMD /install.sh;/usr/bin/supervisord -c /etc/supervisor/supervisord.conf
