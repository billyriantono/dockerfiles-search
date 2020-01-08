FROM ibmcom/websphere-traditional:9.0.0.6-profile

USER root

ENV JAVA_HOME /opt/IBM/WebSphere/AppServer/java/8.0

# http://webproxy-utvikler.nav.no:8088
ARG http_proxy=""
ARG no_proxy=155.55.,192.168.,10.,local,rtv.gov,adeo.no,nav.no,aetat.no,devillo.no,oera.no

ENV http_proxy ${http_proxy}
ENV https_proxy ${http_proxy}
ENV no_proxy ${no_proxy}

RUN (test -n "${http_proxy}" && echo "Acquire::http::Proxy \"${http_proxy}\";Acquire::https::Verify-Peer \"true\";Acquire::https::Verify-Host \"true\";" > /etc/apt/apt.conf.d/proxy.conf) || true

COPY webproxy.crt /usr/local/share/ca-certificates/
RUN update-ca-certificates

ARG MAVEN_VERSION=3.3.9
ARG USER_HOME_DIR="/root"
ARG SHA=6e3e9c949ab4695a204f74038717aa7b2689b1be94875899ac1b3fe42800ff82
ARG BASE_URL=https://apache.uib.no/maven/maven-3/${MAVEN_VERSION}/binaries

RUN (apt-get update || true) && apt-get install -y curl \
  && mkdir -p /usr/share/maven /usr/share/maven/ref \
  && curl -fsSL -o /tmp/apache-maven.tar.gz ${BASE_URL}/apache-maven-${MAVEN_VERSION}-bin.tar.gz \
  && echo "${SHA}  /tmp/apache-maven.tar.gz" | sha256sum -c - \
  && tar -xzf /tmp/apache-maven.tar.gz -C /usr/share/maven --strip-components=1 \
  && rm -f /tmp/apache-maven.tar.gz \
  && ln -s /usr/share/maven/bin/mvn /usr/bin/mvn

ENV MAVEN_HOME /usr/share/maven
ENV MAVEN_CONFIG "$USER_HOME_DIR/.m2"

ENV NEXUS_USERNAME=""
ENV NEXUS_PASSWORD=""

COPY mvn-entrypoint.sh /usr/local/bin/mvn-entrypoint.sh
COPY settings.xml /usr/share/maven/ref/
COPY toolchains.xml /usr/share/maven/ref/

ENTRYPOINT ["/usr/local/bin/mvn-entrypoint.sh"]
CMD ["mvn"]
