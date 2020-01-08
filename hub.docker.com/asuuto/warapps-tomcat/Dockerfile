FROM tomcat:7-jre8-alpine
MAINTAINER Nate Wilken <wilken@asu.edu>

ENV DOCKER_BASE_VERSION=0.0.4
ENV CONSUL_TEMPLATE_VERSION=0.19.5
ENV NEWRELIC_VERSION=4.12.0

ENV HASHICORP_RELEASES=https://releases.hashicorp.com
ENV NEWRELIC_RELEASES=https://download.newrelic.com

RUN apk add --no-cache bash ca-certificates curl gnupg libcap openssl jq && \
    gpg --keyserver ha.pool.sks-keyservers.net --recv-keys 91A6E7F85D05C65630BEF18951852D87348FFC4C && \
    mkdir -p /tmp/build && \
    cd /tmp/build && \
    wget ${HASHICORP_RELEASES}/docker-base/${DOCKER_BASE_VERSION}/docker-base_${DOCKER_BASE_VERSION}_linux_amd64.zip && \
    wget ${HASHICORP_RELEASES}/docker-base/${DOCKER_BASE_VERSION}/docker-base_${DOCKER_BASE_VERSION}_SHA256SUMS && \
    wget ${HASHICORP_RELEASES}/docker-base/${DOCKER_BASE_VERSION}/docker-base_${DOCKER_BASE_VERSION}_SHA256SUMS.sig && \
    gpg --batch --verify docker-base_${DOCKER_BASE_VERSION}_SHA256SUMS.sig docker-base_${DOCKER_BASE_VERSION}_SHA256SUMS && \
    grep ${DOCKER_BASE_VERSION}_linux_amd64.zip docker-base_${DOCKER_BASE_VERSION}_SHA256SUMS | sha256sum -c && \
    unzip docker-base_${DOCKER_BASE_VERSION}_linux_amd64.zip && \
    cp bin/gosu bin/dumb-init /bin && \
    wget ${HASHICORP_RELEASES}/consul-template/${CONSUL_TEMPLATE_VERSION}/consul-template_${CONSUL_TEMPLATE_VERSION}_linux_amd64.zip && \
    wget ${HASHICORP_RELEASES}/consul-template/${CONSUL_TEMPLATE_VERSION}/consul-template_${CONSUL_TEMPLATE_VERSION}_SHA256SUMS && \
    wget ${HASHICORP_RELEASES}/consul-template/${CONSUL_TEMPLATE_VERSION}/consul-template_${CONSUL_TEMPLATE_VERSION}_SHA256SUMS.sig && \
    gpg --batch --verify consul-template_${CONSUL_TEMPLATE_VERSION}_SHA256SUMS.sig consul-template_${CONSUL_TEMPLATE_VERSION}_SHA256SUMS && \
    grep consul-template_${CONSUL_TEMPLATE_VERSION}_linux_amd64.zip consul-template_${CONSUL_TEMPLATE_VERSION}_SHA256SUMS | sha256sum -c && \
    unzip -d /bin consul-template_${CONSUL_TEMPLATE_VERSION}_linux_amd64.zip && \
    cd /tmp && \
    rm -rf /tmp/build && \
    wget ${NEWRELIC_RELEASES}/newrelic/java-agent/newrelic-agent/${NEWRELIC_VERSION}/newrelic-java.zip && \
    unzip -d /usr/local newrelic-java.zip && \
    rm newrelic-java.zip && \
    apk del gnupg openssl && \
    rm -rf /root/.gnupg

# The agent will be started with /consul-template/config as the configuration directory
# so you can add additional config files in that location.
RUN mkdir -p /consul-template/config

COPY server.xml ${CATALINA_HOME}/conf/server.xml
COPY logging.properties ${CATALINA_HOME}/conf/logging.properties
COPY lib/*.jar ${CATALINA_HOME}/lib/

VOLUME ${CATALINA_HOME}/logs

RUN rm -rf ${CATALINA_HOME}/webapps/*

EXPOSE 8080

COPY entrypoint.sh /usr/local/bin/entrypoint.sh
RUN chmod 555 /usr/local/bin/entrypoint.sh
ENTRYPOINT ["/usr/local/bin/entrypoint.sh"]

CMD ["catalina.sh", "run"]
