FROM nginx
MAINTAINER mauricio.van.der.maesen@iqu.com

# https://www.digitalocean.com/community/tutorials/how-to-secure-nginx-with-let-s-encrypt-on-ubuntu-14-04

RUN apt-get update 
RUN apt-get install -y wget

RUN cd /usr/local/sbin && wget https://dl.eff.org/certbot-auto && chmod a+x /usr/local/sbin/certbot-auto

# Generate Strong Diffie-Hellman Group
RUN openssl dhparam -out /etc/ssl/certs/dhparam.pem 2048


