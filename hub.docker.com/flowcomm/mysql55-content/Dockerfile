
FROM eclipse/centos_jdk8
USER root
RUN wget -qO- "https://github.com/apache/incubator-openwhisk-cli/releases/download/latest/OpenWhisk_CLI-latest-linux-amd64.tgz" | tar -zx -C /usr/local/bin/ && \
    wget -qO- "https://github.com/apache/incubator-openwhisk-wskdeploy/releases/download/0.9.0/wskdeploy-0.9.0-linux-amd64.tgz" | tar -zx -C /usr/local/bin/
USER user
RUN cd /tmp && git clone https://github.com/jboss-fuse/fuse-springboot-circuit-breaker-booster && cd fuse-springboot-circuit-breaker-booster && mvn clean package && rm -rf /tmp/fuse-springboot-circuit-breaker-booster
