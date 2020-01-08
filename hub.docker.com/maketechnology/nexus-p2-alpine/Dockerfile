FROM rawmind/alpine-nexus:2.12.1-01

RUN NEXUS_VERSION=2.12.1-01 \
 && MVN_URL=http://search.maven.org/remotecontent?filepath=org/sonatype/nexus/plugins \
 && mkdir -p ${SERVICE_WORK}/plugin-repository/ \
 && curl -jksSL ${MVN_URL}/nexus-p2-repository-plugin/${NEXUS_VERSION}/nexus-p2-repository-plugin-${NEXUS_VERSION}-bundle.zip -o /tmp/nexus-p2-repository-plugin-bundle.zip \
 && unzip /tmp/nexus-p2-repository-plugin-bundle.zip -d ${SERVICE_WORK}/plugin-repository/ \
 && rm -rf /tmp/nexus-p2-repository-plugin-bundle.zip \
 && curl -jksSL ${MVN_URL}/nexus-p2-bridge-plugin/${NEXUS_VERSION}/nexus-p2-bridge-plugin-${NEXUS_VERSION}-bundle.zip -o /tmp/nexus-p2-bridge-plugin-bundle.zip \
 && unzip /tmp/nexus-p2-bridge-plugin-bundle.zip -d ${SERVICE_WORK}/plugin-repository/ \
 && rm -rf /tmp/nexus-p2-repository-plugin-bundle.zip
