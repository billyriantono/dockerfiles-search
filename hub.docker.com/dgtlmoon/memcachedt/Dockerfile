FROM alpine:3.10

#-----------

### Install Nano Editor ###
ENV LANG="en_US.UTF-8" \
    LC_ALL="en_US.UTF-8" \
    LANGUAGE="en_US.UTF-8"

RUN apk -U upgrade && \
    apk --update add nano && \
    rm -rf /var/cache/apk/*
    
#-------------------- 


# install supervisord para gerenciar multiplos processos (aplicativos) em um único contêiner
RUN apk add --update supervisor && rm  -rf /tmp/* /var/cache/apk/*

COPY config/supervisord.conf /etc/supervisord.conf

# Install dovecot, rspamd (filtro spam) e Sieve (filtro mail, autoresponde, 
RUN apk add --no-cache \
  dovecot dovecot-lmtpd dovecot-pop3d dovecot-submissiond dovecot-pigeonhole-plugin rspamd-client \
  && mkdir /var/lib/dovecot
  
# Install postfix, rsyslog (monitora logs), ca-certificates, openssl
RUN apk add --no-cache postfix postfix-pcre cyrus-sasl-plain ca-certificates rsyslog openssl

COPY config/rsyslog.conf /etc/rsyslog.conf

COPY config/ssl/ /etc/ssl/

#RUN chmod 0400 /etc/ssl/private/ssl-cert-snakeoil.key

# Install fetchmail e ca-certificates
RUN apk add --no-cache fetchmail \
&& mkdir /etc/fetchmailrc 

# Criando volumes
VOLUME ["/etc/dovecot","/etc/postfix","/vmail"]

# Expondo portas
EXPOSE 25/tcp 587/tcp 2587/tcp 995/tcp 993/tcp 143/tcp

# Executa a lista de aplicativos no supervisord
ENTRYPOINT ["supervisord", "--nodaemon", "--configuration", "/etc/supervisord.conf"]
