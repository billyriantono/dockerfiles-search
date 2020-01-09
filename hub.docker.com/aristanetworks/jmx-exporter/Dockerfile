# Copyright (c) 2019  Arista Networks, Inc.  All rights reserved.
# Arista Networks, Inc. Confidential and Proprietary.

FROM aristanetworks/openjdk:2.1
LABEL maintainer="Fabrice Rabaute fabrice@arista.com"

# Install jxm exporter
ENV JMXP 0.12.0
RUN wget -nv -O /jmx_prometheus_httpserver.jar \
	https://repo1.maven.org/maven2/io/prometheus/jmx/jmx_prometheus_httpserver/${JMXP}/jmx_prometheus_httpserver-${JMXP}-jar-with-dependencies.jar \
	&& echo 6a87ce250b7ee6ea58b2100237389fa69596bb9d35faec9ac4c059411bd61769dcf0c2322241f0b5935254a5740d0e6c330b3abdcdc9c9831057a0d876922d76  /jmx_prometheus_httpserver.jar | sha512sum -c - \
	&& wget -nv -O /jmx_prometheus_javaagent.jar \
	https://repo1.maven.org/maven2/io/prometheus/jmx/jmx_prometheus_javaagent/${JMXP}/jmx_prometheus_javaagent-${JMXP}.jar \
	&& echo 17d275cca87eb5d593cc31ffa704587c0e867c8ae6e1eab0a5a54598bbb84b79ba3f7fad26ef6b3f2fa2f05ffee61c2d733dfb9536d2b067ecd37f485330b5e8  /jmx_prometheus_javaagent.jar | sha512sum -c -

ENTRYPOINT ["/usr/bin/dumb-init", "--", "java", "-jar", "/jmx_prometheus_httpserver.jar"]
CMD ["7071", "/jmx-exporter-config.yml"]
