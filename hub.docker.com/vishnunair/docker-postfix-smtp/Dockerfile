From debian:latest

MAINTAINER Vishnu Nair <me@vishnudxb.me>

COPY policy-rc.d  /usr/sbin/policy-rc.d

RUN apt-get update && \
    DEBIAN_FRONTEND=noninteractive apt-get -y --force-yes -qq install mailutils postfix libsasl2-2 ca-certificates libsasl2-modules 

COPY sasl_passwd /etc/postfix/
COPY postfix.sh  /bin/
COPY postfix-main.cf /etc/postfix/postfix-main.cf

RUN  sed -i 's/relayhost/#relayhost/g' /etc/postfix/main.cf && \
     echo example.com > /etc/mailname && \
     cat /etc/postfix/postfix-main.cf >> /etc/postfix/main.cf && \
     chmod +x /bin/postfix.sh /usr/sbin/policy-rc.d 

EXPOSE 587

CMD . /bin/postfix.sh 
