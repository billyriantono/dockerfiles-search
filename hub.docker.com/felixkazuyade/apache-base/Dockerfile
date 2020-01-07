FROM felixkazuyade/base-image
RUN echo "Built at" $(date) > /etc/built_at

# Add generic ansible roles
COPY entrypoint /entrypoint
RUN chmod +x /entrypoint

#RUN ansible-playbook container.yml -c local
# apt-get update is done by base-image
RUN apt-get update 
RUN apt-get  -yq install apache2           
RUN apt-get  -yq install libapache2-mod-auth-kerb
RUN apt-get  -yq install libapache2-mod-php
RUN apt-get  -yq install php
RUN apt-get  -yq install php-mysql
RUN apt-get  -yq install php-intl
RUN apt-get  -yq install php-ldap
RUN apt-get  -yq install php7.0-mysql
RUN apt-get  -yq install libapache2-mod-php7.0
RUN apt-get  -yq install php7.0-mcrypt
RUN apt-get  -yq install php7.0-curl
RUN apt-get  -yq install php7.0-xml
RUN apt-get  -yq install php7.0-mbstring
RUN apt-get  -yq install php7.0-zip
RUN apt-get  -yq install hp7.0-ldap


RUN ln -sf /proc/self/fd/1 /var/log/apache2/access.log 
RUN ln -sf /proc/self/fd/1 /var/log/apache2/error.log 
RUN ln -sf /proc/self/fd/1 /var/log/apache2/ssl_access.log 
RUN ln -sf /proc/self/fd/1 /var/log/apache2/other_vhosts_access.log 

#RUN a2dismod auth_kerb php7.0 
#RUN phpdismod mysqli zip xml ldap mcrypt curl mbstring

WORKDIR /var/www/html/

EXPOSE 80
EXPOSE 443

CMD [ "/entrypoint"]
