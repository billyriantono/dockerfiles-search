FROM centos:7

LABEL MAINTAINER aladin-29

RUN yum -y update && yum install -y postfix \
    rsyslog \
    mailx \
    cyrus-sasl \
    cyrus-sasl-plain \
    stunnel \
    && yum clean all;


#postfix configuration 

#main.cf 
RUN echo -e "myhostname = relay-mail.postfix.docker\n\
smtp_sasl_auth_enable=yes\n\
smtp_sasl_security_options=\n\
relayhost=[127.0.0.1]:11125\n\
smtp_sasl_password_maps=hash:/etc/postfix/sasl_passwd\n\
sender_canonical_maps =pcre:/etc/postfix/canonical" >> /etc/postfix/main.cf \


#tcp wrapper configuration
&& echo -e "[smtp-tls-wrapper]\n\
  accept = 11125\n\
  client = yes " >> /etc/stunnel/stunnel.conf \

#rsyslog configuration ---> This needs to enable postfix logs inside container 
&& rm -f /etc/rsyslog.d/listen.conf \
&& sed -i '/$ModLoad imjournal/d' /etc/rsyslog.conf \
&& sed -i '/$IMJournalStateFile/d' /etc/rsyslog.conf \
&& sed -i '/$OmitLocalLogging on/c $OmitLocalLogging off' /etc/rsyslog.conf;


#adding the scripts 
ADD run.sh	/root/run.sh
RUN chmod 700 /root/run.sh

#Declare variables
ENV  SMTP_LOGIN=aladin29@email-adress.com \ 
     SMTP_PASSWORD=aladin-password\
     SERVER=smtp.aladin.com 

#port declare
EXPOSE 25

#script run the services --> postfix and rsyslog and stunnel
CMD bash -C '/root/run.sh';'bash'


