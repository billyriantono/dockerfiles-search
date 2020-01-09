FROM faboulaye/openjdk:alpine
MAINTAINER Firdaws Aboulaye <aboufred@gmail.com>

ENV SONAR_VERSION=6.0
ENV SONARQUBE_HOME=/opt/sonarqube
# Database configuration - Defaults to using H2
ENV SONARQUBE_JDBC_USERNAME=sonar
ENV SONARQUBE_JDBC_PASSWORD=sonar
ENV SONARQUBE_JDBC_URL=

COPY docker-entrypoint.sh /

RUN apk add --update --no-cache gnupg unzip curl \
  && cd /tmp \
  && gpg --keyserver ha.pool.sks-keyservers.net --recv-keys F1182E81C792928921DBCAB4CFCA4A29D26468DE \
  && curl -o sonarqube.zip -fSL https://sonarsource.bintray.com/Distribution/sonarqube/sonarqube-$SONAR_VERSION.zip \
  && curl -o sonarqube.zip.asc -fSL https://sonarsource.bintray.com/Distribution/sonarqube/sonarqube-$SONAR_VERSION.zip.asc \
  && gpg --batch --verify sonarqube.zip.asc sonarqube.zip \
  && unzip sonarqube.zip \
  && mkdir /opt \
  && mv sonarqube-$SONAR_VERSION $SONARQUBE_HOME \
  && chmod +x /docker-entrypoint.sh \
  && apk del gnupg unzip curl \
  && rm -rf sonarqube.zip* /var/cache/apk/* /tmp/*

VOLUME ["$SONARQUBE_HOME/data", "$SONARQUBE_HOME/extensions"]
EXPOSE 9000
WORKDIR $SONARQUBE_HOME

ENTRYPOINT ["/docker-entrypoint.sh"]
