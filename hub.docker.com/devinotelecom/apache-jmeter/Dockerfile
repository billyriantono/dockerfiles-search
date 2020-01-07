FROM openjdk:8u212-jre-alpine3.9

ENV APACHE_JMETER_VERSION=5.1.1

RUN set -ex && \
    cd /tmp/ && \
    wget -q https://archive.apache.org/dist/jmeter/KEYS && \
    wget -q https://archive.apache.org/dist/jmeter/binaries/apache-jmeter-${APACHE_JMETER_VERSION}.tgz && \
    wget -q https://archive.apache.org/dist/jmeter/binaries/apache-jmeter-${APACHE_JMETER_VERSION}.tgz.asc && \
    \
    apk add --no-cache gnupg && \
    gpg --quiet --import KEYS && \
    gpg --verify apache-jmeter-${APACHE_JMETER_VERSION}.tgz.asc apache-jmeter-${APACHE_JMETER_VERSION}.tgz && \
    \
    tar xzf apache-jmeter-${APACHE_JMETER_VERSION}.tgz && \
    mv apache-jmeter-${APACHE_JMETER_VERSION} /opt/apache-jmeter && \
    \
    rm -rf /tmp/* \
        /opt/apache-jmeter/NOTICE \
        /opt/apache-jmeter/README.md \
        /opt/apache-jmeter/docs \
        /opt/apache-jmeter/extras \
        /opt/apache-jmeter/printable_docs \
        /opt/apache-jmeter/bin/examples \
        /opt/apache-jmeter/bin/*.bat \
        /opt/apache-jmeter/bin/*.cmd \
        /opt/apache-jmeter/bin/*.bshrc

COPY log4j2.xml /opt/apache-jmeter/bin/log4j2.xml

ENTRYPOINT ["/opt/apache-jmeter/bin/jmeter"]
