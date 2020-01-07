FROM httpd:alpine

ENV JAVA_OPTS="-XX:+UnlockExperimentalVMOptions -XX:+UseCGroupMemoryLimitForHeap" \
  MIRROR_DIRECTORY="/usr/local/apache2/htdocs/" \
  NIST_DATA_MIRROR_VERSION=1.4.0

COPY root/ /

RUN apk add --no-cache openjdk8-jre \
  && rm -f /usr/local/apache2/htdocs/*.html \
  && ln -s /usr/local/bin/nvd-update /etc/periodic/daily/nvd-update

ADD https://repo1.maven.org/maven2/us/springett/nist-data-mirror/${NIST_DATA_MIRROR_VERSION}/nist-data-mirror-${NIST_DATA_MIRROR_VERSION}.jar /usr/local/bin/nist-data-mirror.jar
