FROM fedora:latest

LABEL maitainer="Luiz Fernando Pereira <luizfernandopereira@outlook.com.br>" \
      company="Alternativa Informática <desenvolvimento@altinfo.com.br>"

RUN dnf -y install \
    java-openjdk \
    && dnf clean all

ENV TINI_VERSION v0.18.0
ADD https://github.com/krallin/tini/releases/download/${TINI_VERSION}/tini /sbin/tini
RUN chmod +x /sbin/tini

RUN curl https://repo1.maven.org/maven2/org/flywaydb/flyway-commandline/6.1.0/flyway-commandline-6.1.0-linux-x64.tar.gz \
    --output /tmp/flyway.tar.gz \
    && tar -xvzf /tmp/flyway.tar.gz -C /tmp \
    && mv /tmp/flyway-6.1.0 /opt/flyway \
    && rm -Rf /opt/flyway/jre

ENV PATH="/opt/flyway:${PATH}"
ENV JAVA_HOME="/etc/alternatives/jre"

COPY entrypoint.sh /entrypoint.sh
RUN chmod +x /entrypoint.sh \
    && mkdir -p /flyway

WORKDIR /flyway

ENTRYPOINT ["/bin/sh", "/entrypoint.sh"]

CMD ["composer"]