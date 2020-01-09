FROM openjdk:11-jdk

ARG EAZYBI_VERSION=5.0.2
ENV EAZYBI_PREFIX=/eazybi

RUN wget -q -O /tmp/eazybi.zip https://eazybi.com/system/downloads/eazybi_private-$EAZYBI_VERSION.zip && \
    unzip /tmp/eazybi.zip -d /opt && \
    rm -rf /tmp/eazybi.zip && \
    sed -i "s|^EAZYBI_HOST=.*$|EAZYBI_HOST=\"0.0.0.0\"|g" /opt/eazybi_private/bin/start.sh

VOLUME [ "/opt/eazybi_private/config" ]
EXPOSE 8080
ENTRYPOINT [ "/opt/eazybi_private/bin/start.sh" ]