FROM debian:stable-slim

RUN apt-get -y update && apt-get -y install vim git rsync python-pip wget tar && apt-get -y clean
COPY certupdate /usr/local/bin/certupdate
COPY certrequest /usr/local/bin/certrequest
COPY certcombine /usr/local/bin/certcombine
COPY certcopy /usr/local/bin/certcopy
COPY selfsign /usr/local/bin/selfsign
RUN wget https://dl.eff.org/certbot-auto \
  && chmod a+x certbot-auto && mv certbot-auto /usr/local/bin/ \ 
  && certbot-auto -tn --agree-tos plugins \
  && chmod a+x /usr/local/bin/certrequest \
  && chmod a+x /usr/local/bin/certupdate \
  && chmod a+x /usr/local/bin/certcombine \
  && chmod a+x /usr/local/bin/certcopy \
  && chmod a+x /usr/local/bin/selfsign
COPY openssl.cnf /openssl.cnf
