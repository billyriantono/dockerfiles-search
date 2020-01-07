# Nginx Full
FROM nginx
MAINTAINER An0t8

#########################################
##          INSTALL NGINX FULL         ##
#########################################

RUN \
# Install packages needed for app
export DEBCONF_NONINTERACTIVE_SEEN=true DEBIAN_FRONTEND=noninteractive && \
apt-get update && \
apt-get -y install nginx-full apache2-utils


RUN \
rm /etc/nginx/nginx.conf

EXPOSE 80 443
