FROM kidac/tomcat:8.5.45.1936

LABEL de.kdac.cas.maintainer = "Claus Böhmer" \
      de.kdac.cas.authors = "eso@bistum-eichstaett.de" \
      de.kdac.cas.url = "https://hub.docker.com/r/kidac/cas" \
      de.kdac.cas.documentation = "https://hub.docker.com/r/kidac/cas" \
      de.kdac.cas.source = "https://github.com/kidac/cas" \
      de.kdac.cas.version = "5.3.12" \
      de.kdac.cas.vendor = "KDAC - https://ews.kdac.de" \
      de.kdac.cas.licenses = "https://www.apereo.org/content/cas-under-apache-20-license" \
      de.kdac.cas.title = "CAS (KDAC Version)" \
      de.kdac.cas.description = "Adapted CAS Dockerfile used by KDAC"

ENV CAS_VERSION=5.3.12

WORKDIR /tmp

RUN apk upgrade --update --no-cache \
 && apk add --no-cache curl openssl libressl2.7-libcrypto nss zip

COPY entrypoint.sh /entrypoint.sh
ADD https://github.com/kidac/cas/raw/master/binary/cas.war /opt/tomcat/webapps/cas.war

RUN rm -rf $CATALINA_HOME/webapps/ROOT \
 && rm -rf $CATALINA_HOME/webapps/docs \
 && rm -rf $CATALINA_HOME/webapps/examples \
 && rm -rf $CATALINA_HOME/webapps/host-manager \
 && rm -rf $CATALINA_HOME/webapps/manager

ENTRYPOINT /entrypoint.sh
