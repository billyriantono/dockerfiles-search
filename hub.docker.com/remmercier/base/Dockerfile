FROM tomcat:8.5.11-jre8
LABEL maintainer "Rémi Mercier <rem.mercier@gmail.com>"

# remove default apps and set timezone
RUN rm -fr /usr/local/tomcat/webapps \
 && mkdir /usr/local/tomcat/webapps \
 && echo "America/Toronto" > /etc/timezone \
 && dpkg-reconfigure -f noninteractive tzdata


