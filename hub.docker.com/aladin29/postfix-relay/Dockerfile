FROM centos

LABEL MAINTAINER aladin-29

RUN yum -y update && \
        yum install postfix -y && yum install rsyslog -y && yum install mailx -y \
        && yum install cyrus-sasl -y && yum install cyrus-sasl-plain -y && \
	yum install stunnel -y;


#postfix configuration 
RUN rm -f /etc/postfix/sasl_passwd 
RUN rm -f /etc/postfix/main.cf
RUN rm -f /etc/postfix/master.cf

ADD main.cf 	/etc/postfix/main.cf
ADD master.cf 	/etc/postfix/master.cf

RUN chmod 700 -R /etc/postfix/

#tcp wrapper configuration
ADD stunnel.conf /etc/stunnel/stunnel.conf

#rsyslog configuration
RUN rm -f /etc/rsyslog.d/listen.conf 
RUN rm -f /etc/rsyslog.conf

ADD rsyslog.conf	/etc/rsyslog.conf


#adding the scripts 
ADD run.sh	/root/run.sh
RUN chmod 700 /root/run.sh

#Declare variables
ENV  SMTP_LOGIN= \ 
     SMTP_PASSWORD= \
     SERVER= 



#port declare
EXPOSE 25

#script run the services --> postfix and rsyslog
#CMD ["/bin/bash/","-c","/root/run.sh"]
CMD bash -C '/root/run.sh';'bash'

