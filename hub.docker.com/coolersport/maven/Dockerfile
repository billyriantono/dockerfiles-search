FROM anapsix/alpine-java:7_jdk

ARG MAVEN_VERSION=3.2.5
ARG USER_HOME_DIR="/root"
ARG SHA=41009327d5494e0e8970b25b77ffed8934cd7ca1
ARG BASE_URL=https://apache.osuosl.org/maven/maven-3/${MAVEN_VERSION}/binaries

# upgrade tar, install curl and git
RUN apk add --update tar curl git \
  && rm -rf /var/cache/apk/* \
# install docker to run docker commands inside this container
  && curl -fsSLO https://download.docker.com/linux/static/stable/x86_64/docker-18.09.4.tgz \
  && tar --strip-components=1 -xvzf docker-18.09.4.tgz -C /usr/local/bin \
# install maven
  && mkdir -p /usr/share/maven /usr/share/maven/ref \
  && curl -fsSL -o /tmp/apache-maven.tar.gz ${BASE_URL}/apache-maven-${MAVEN_VERSION}-bin.tar.gz \
  && echo "${SHA}  /tmp/apache-maven.tar.gz" | sha1sum -c - \
  && tar -xzf /tmp/apache-maven.tar.gz -C /usr/share/maven --strip-components=1 \
  && rm -f /tmp/apache-maven.tar.gz \
  && ln -s /usr/share/maven/bin/mvn /usr/bin/mvn

ENV LC_ALL C
ENV MAVEN_HOME /usr/share/maven
ENV MAVEN_CONFIG "$USER_HOME_DIR/.m2"

COPY mvn-entrypoint.sh /usr/local/bin/mvn-entrypoint.sh
COPY settings-docker.xml /usr/share/maven/ref/

VOLUME "$USER_HOME_DIR/.m2"

ENTRYPOINT ["/usr/local/bin/mvn-entrypoint.sh"]
CMD ["mvn"]
