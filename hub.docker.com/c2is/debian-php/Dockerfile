FROM php:7.0.31-fpm-stretch

MAINTAINER André Cianfarani <a.cianfarani@c2is.fr>

RUN apt-get update && \ 
 apt-get install -y ssmtp && \   
 apt-get clean && \
 echo "FromLineOverride=YES" >> /etc/ssmtp/ssmtp.conf && \
 echo "root=postmaster" >> /etc/ssmtp/ssmtp.conf && \
 echo "mailhub=mail" >> /etc/ssmtp/ssmtp.conf && \
 echo "AuthUser=web" >> /etc/ssmtp/ssmtp.conf && \
 echo "AuthPass=web" >> /etc/ssmtp/ssmtp.conf && \
 echo "hostname=acti.fr" >> /etc/ssmtp/ssmtp.conf && \
 echo "root:web:mail" >> /etc/ssmtp/revaliases && \
 echo 'sendmail_path = "/usr/sbin/ssmtp -t"' > /usr/local/etc/php/conf.d/mail.ini


