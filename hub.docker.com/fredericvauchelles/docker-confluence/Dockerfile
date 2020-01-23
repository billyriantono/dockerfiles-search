FROM debian:latest

# Setup useful environment variables
ENV CONF_HOME             /var/atlassian/confluence
ENV CONF_INSTALL          /opt/atlassian/confluence
ENV CONF_VERSION          5.9.14
ENV JAVA_FILE_VERSION     8u71
ENV JAVA_DISTRIB_VERSION  b15
ENV JAVA_VERSION          1.8.0_71

# grab gosu for easy step-down from root
RUN gpg --keyserver ha.pool.sks-keyservers.net --recv-keys B42F6819007F00F88E364FD4036A9C25BF357DD4
RUN apt-get update && apt-get install -y --no-install-recommends ca-certificates wget && rm -rf /var/lib/apt/lists/* \
    && wget -O /usr/local/bin/gosu "https://github.com/tianon/gosu/releases/download/1.2/gosu-$(dpkg --print-architecture)" \
    && wget -O /usr/local/bin/gosu.asc "https://github.com/tianon/gosu/releases/download/1.2/gosu-$(dpkg --print-architecture).asc" \
    && gpg --verify /usr/local/bin/gosu.asc \
    && rm /usr/local/bin/gosu.asc \
    && chmod +x /usr/local/bin/gosu \
    && apt-get purge -y --auto-remove ca-certificates wget

# Create user
RUN   groupadd -r confluence --gid=999 \
   && useradd -r -g confluence --uid=999 confluence

# Install curl
RUN   apt-get --quiet update \
  &&  apt-get -y install curl

# Install java
# https://www.digitalocean.com/community/tutorials/how-to-manually-install-oracle-java-on-a-debian-or-ubuntu-vps
RUN   curl -#LO --header "Cookie: oraclelicense=accept-securebackup-cookie" http://download.oracle.com/otn-pub/java/jdk/${JAVA_FILE_VERSION}-${JAVA_DISTRIB_VERSION}/jdk-${JAVA_FILE_VERSION}-linux-x64.tar.gz \
  &&  mkdir -p /opt/jdk \
  &&  tar -zxf jdk-${JAVA_FILE_VERSION}-linux-x64.tar.gz -C /opt/jdk \
  &&  rm jdk-${JAVA_FILE_VERSION}-linux-x64.tar.gz \
  &&  update-alternatives --install /usr/bin/java java /opt/jdk/jdk${JAVA_VERSION}/bin/java 100 \
  &&  update-alternatives --install /usr/bin/javac javac /opt/jdk/jdk${JAVA_VERSION}/bin/javac 100 \
  &&  export JAVA_HOME=/opt/jdk/jdk${JAVA_VERSION}/

# Create confluence directories
RUN   mkdir -p                "${CONF_HOME}" \
  &&  chown -R confluence:    "${CONF_HOME}" \
  &&  chmod -R 700            "${CONF_HOME}" \
  &&  mkdir -p                "${CONF_INSTALL}/conf"

# Download and install confluence
RUN   curl -Ls                "https://downloads.atlassian.com/software/confluence/downloads/atlassian-confluence-${CONF_VERSION}.tar.gz" \
  |   tar -xz --directory "${CONF_INSTALL}" --strip-components=1 --no-same-owner 

# Setup configuration
RUN  echo -e                 "\nconfluence.home=$CONF_HOME" >> "${CONF_INSTALL}/confluence/WEB-INF/classes/confluence-init.properties" 

# Setup permissions
RUN   chown -R confluence:    "${CONF_INSTALL}/conf" \
  &&  chown -R confluence:    "${CONF_INSTALL}/temp" \
  &&  chown -R confluence:    "${CONF_INSTALL}/logs" \
  &&  chown -R confluence:    "${CONF_INSTALL}/work" \
  &&  chmod -R 700            "${CONF_INSTALL}/conf" \
  &&  chmod -R 700            "${CONF_INSTALL}/temp" \
  &&  chmod -R 700            "${CONF_INSTALL}/logs" \
  &&  chmod -R 700            "${CONF_INSTALL}/work" 

COPY docker-entrypoint.sh /
RUN  chown confluence: docker-entrypoint.sh \
  && chmod 700 docker-entrypoint.sh

EXPOSE 8090
VOLUME ["/var/atlassian/confluence"]
WORKDIR ${CONF_HOME}

ENTRYPOINT ["/docker-entrypoint.sh"]