FROM jschnabel/nginx-php7:1.0

LABEL Maintainer="Joshua Schnabel <dev@joshua-schnabel.de>" \
      Description="DAViCal Container with external PostgreSQL connector"      
      
# Switch to use root user for setup
USER root
      
RUN apk update && apk upgrade && \
    apk add --no-cache php7-pgsql php7-imap php7-curl php7-cgi php7-xml bash git openssh postgresql-client perl-dbi perl-yaml-libyaml perl-dbd-pg
    
RUN cd /tmp  && \
    git clone https://gitlab.com/davical-project/davical.git ; \
    git clone https://gitlab.com/davical-project/awl.git ; \
    rm -rf /tmp/davical/.git/ ; \
    rm -rf /tmp/awl/.git/

RUN cd /tmp  && \
    mv davical/ /usr/share/ && \
    mv awl/ /usr/share/ && \    
    chown -R root:www-data /usr/share/davical && \
    cd /usr/share/davical/ && \
    find ./ -type d -exec chmod u=rwx,g=rx,o= '{}' \;  && \
    find ./ -type f -exec chmod u=rw,g=r,o= '{}' \;  && \
    chown -R root:www-data /usr/share/awl  && \
    cd /usr/share/awl/  && \
    find ./ -type d -exec chmod u=rwx,g=rx,o= '{}' \;  && \
    find ./ -type f -exec chmod u=rw,g=r,o= '{}' \;
	
COPY entrypoint-davical.sh /usr/local/bin/

RUN chmod +x /usr/local/bin/entrypoint-davical.sh

ENTRYPOINT ["entrypoint-davical.sh"]
CMD ["nginx", "-g", "daemon off;"]