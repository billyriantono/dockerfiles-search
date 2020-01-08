FROM openjdk:8-jdk-alpine

RUN apk --update --no-cache add bash \
&& rm -rf /var/cache/apk/* \
&& mkdir /usr/share/liquibase \
&& mkdir /driver \
&& mkdir /migrations \
&& wget -O - https://github.com/liquibase/liquibase/releases/download/liquibase-parent-3.6.2/liquibase-3.6.2-bin.tar.gz | tar -zxf - -C /usr/share/liquibase \
&& wget http://central.maven.org/maven2/org/slf4j/slf4j-api/1.7.25/slf4j-api-1.7.25.jar -P /usr/share/liquibase/lib \
&& chmod +x /usr/share/liquibase/liquibase \
&& ln -s /usr/share/liquibase/liquibase /usr/local/bin/ \
&& wget -O /driver/postgresql-42.2.4.jar https://jdbc.postgresql.org/download/postgresql-42.2.4.jar \
&& printf '#!/bin/bash \n\
liquibase --driver=org.postgresql.Driver --classpath=/driver/postgresql-42.2.4.jar "$@"' > /usr/local/bin/liq \
&& chmod +x /usr/local/bin/liq

WORKDIR /migrations