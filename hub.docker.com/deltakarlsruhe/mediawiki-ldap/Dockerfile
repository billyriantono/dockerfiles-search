FROM  	mediawiki:1.27.3 

RUN \
  echo "deb http://packages.dotdeb.org jessie all" >> /etc/apt/sources.list && \
  echo 'deb-src http://packages.dotdeb.org jessie all' >> /etc/apt/sources.list && \
  curl -O https://www.dotdeb.org/dotdeb.gpg && \
  apt-key add dotdeb.gpg && \
  rm dotdeb.gpg
  
RUN apt-get -qq update && \
  apt-get -yqq install php7.0-ldap libldap2-dev
  
RUN docker-php-ext-configure ldap --with-libdir=lib/x86_64-linux-gnu/ && \
    docker-php-ext-install ldap
    
# RUN set -x && \
#     sed -i 's/rtrim/trim/' /var/www/html/extensions/LdapAuthentication/LdapAuthentication.php
