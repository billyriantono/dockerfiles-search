# Build custom ActiveMQ image with jmx_exporter instrumentation to allow scaping metrics by Prometheus.
# Based on rmohr's activemq Dockerfile.
# See https://github.com/rmohr/docker-activemq.
# See https://github.com/prometheus/jmx_exporter.

FROM rmohr/activemq:5.15.6-alpine

MAINTAINER Marcus Geiger <marcus.geiger@spqr-info.de>

ENV AGENT_VERSION=0.3.0
ENV AGENT_SHA512=af1abc5e9412e62f767d2ece00930b08e749278030ff26a690d721c707b526ca1f99731e75a4f23f5080e7f57b4d61c3e3f8d510b7c0e998e1eb397b1e1ac08c
ENV AGENT_BASE=jmx_prometheus_javaagent
ENV AGENT=$AGENT_BASE-$AGENT_VERSION.jar
ENV AGENT_CONFIG=config.yaml
ENV AGENT_PORT=8080
ENV AGENT_OPTS="-javaagent:/$AGENT=$AGENT_PORT:/config.yaml"

ADD https://repo1.maven.org/maven2/io/prometheus/jmx/$AGENT_BASE/$AGENT_VERSION/$AGENT /
USER root
RUN chmod 0644 /$AGENT && if [ "$AGENT_SHA512" != "$(cd / && sha512sum $AGENT | awk '{print($1)}')" ]; then \
  echo "Agent sha512 value doesn't match! exiting."  && exit 1; \
  fi
COPY $AGENT_CONFIG /

ENV ACTIVEMQ_DEBUG_OPTS="$AGENT_OPTS"
