FROM jenkins/jenkins:alpine

USER root

RUN apk --update --no-cache add bash sshpass git php7 php7-ctype php7-curl php7-mbstring php7-iconv php7-openssl php7-json php7-phar php7-xml php7-dom nodejs docker make py-pip \
&& pip install docker-compose \
&& apk del make \
&& mkdir /usr/share/liquibase \
   && mkdir /driver \
   && mkdir /migrations \
   && wget -O - https://github.com/liquibase/liquibase/releases/download/liquibase-parent-3.5.3/liquibase-3.5.3-bin.tar.gz | tar -zxf - -C /usr/share/liquibase \
   && chmod +x /usr/share/liquibase/liquibase \
   && ln -s /usr/share/liquibase/liquibase /usr/local/bin/ \
   && wget -O /driver/postgresql-42.1.4.jar https://jdbc.postgresql.org/download/postgresql-42.1.4.jar \
   && printf '#!/bin/bash \n\
   liquibase --driver=org.postgresql.Driver --classpath=/driver/postgresql-42.1.4.jar "$@"' > /usr/local/bin/liq \
   && chmod +x /usr/local/bin/liq \
   && wget -O - https://getcomposer.org/installer | php -- --install-dir=/usr/bin --filename=composer \
   && composer global require hirak/prestissimo