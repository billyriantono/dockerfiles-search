# Copyright (c) 2019  Arista Networks, Inc.  All rights reserved.
# Arista Networks, Inc. Confidential and Proprietary.

FROM openjdk:11.0.3-jdk-stretch
LABEL maintainer="Fabrice Rabaute fabrice@arista.com"

ENV HADOOP_VERSION 2.8.4
ENV JMXP_VERSION 0.11.0

# Install dumb-init
# Install libsnappy for hadoop native support
# Install prometheus jmx exporter
# Install Hadoop
RUN wget -nv https://github.com/Yelp/dumb-init/releases/download/v1.2.2/dumb-init_1.2.2_amd64 -O /usr/bin/dumb-init \
    && echo "37f2c1f0372a45554f1b89924fbb134fc24c3756efaedf11e07f599494e0eff9  /usr/bin/dumb-init" \
        | sha256sum - \
    && chmod +x /usr/bin/dumb-init \
    && apt-get update \
    && apt-get install -y --no-install-recommends libsnappy1v5 \
    && rm -rf /var/lib/apt/lists/* \
    && wget -nv -O /hadoop.tar.gz \
        https://www-us.apache.org/dist/hadoop/common/hadoop-${HADOOP_VERSION}/hadoop-${HADOOP_VERSION}.tar.gz \
    && echo 6b545972fdd73173887cdbc3e1cbd3cc72068271924edea82a0e7e653199b115  /hadoop.tar.gz | sha256sum -c - \
    && tar xf /hadoop.tar.gz -C / \
    && rm /hadoop.tar.gz \
    && ln -s /hadoop-${HADOOP_VERSION} /hadoop \
    && wget -nv -O ${JAVA_HOME}/lib/jmx_prometheus_javaagent.jar \
        https://repo1.maven.org/maven2/io/prometheus/jmx/jmx_prometheus_javaagent/${JMXP_VERSION}/jmx_prometheus_javaagent-${JMXP_VERSION}.jar \
    && echo "0c8e2f7b9753fd540c17546bf1a6bfdbb39747493e02ea8ad8566097607c0c2d  ${JAVA_HOME}/lib/jmx_prometheus_javaagent.jar" \
        | sha256sum -

ENTRYPOINT ["/usr/bin/dumb-init", "--"]
