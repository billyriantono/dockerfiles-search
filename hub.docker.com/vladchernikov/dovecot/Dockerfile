FROM alpine:3.8

RUN apk --no-cache add \
    dovecot=2.3.2.1-r0 \
    dovecot-ldap=2.3.2.1-r0

# IMAP
EXPOSE 143 

# SSL/TLS encrypted IMAP
EXPOSE 993 

# POP
EXPOSE 110 

# SSL/TLS encrypted POP
EXPOSE 995 
 
CMD ["dovecot", "-F", "-c", "/etc/dovecot/dovecot.conf"]
