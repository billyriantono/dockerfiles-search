FROM debian:latest

# Setup useful environment variables
ENV CONF_HOME             /var/atlassian/bamboo
ENV CONF_INSTALL          /opt/atlassian/bamboo
ENV CONF_VERSION          5.13.1
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
RUN   groupadd -r bamboo --gid=999 \
   && useradd -r -g bamboo --uid=999 bamboo

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
  &&  chown -R bamboo:        "${CONF_HOME}" \
  &&  chmod -R 700            "${CONF_HOME}" \
  &&  mkdir -p                "${CONF_INSTALL}/conf"

# Download and install bamboo
RUN   curl -Ls                "https://downloads.atlassian.com/software/bamboo/downloads/atlassian-bamboo-${CONF_VERSION}.tar.gz" \
  |   tar -xz --directory "${CONF_INSTALL}" --strip-components=1 --no-same-owner 

# Setup configuration
RUN  echo -e                 "\nbamboo.home=$CONF_HOME" >> "${CONF_INSTALL}/atlassian-bamboo/WEB-INF/classes/bamboo-init.properties" 

# Setup permissions
RUN   chown -R bamboo:        "${CONF_INSTALL}/conf" \
  &&  chown -R bamboo:        "${CONF_INSTALL}/temp" \
  &&  chown -R bamboo:        "${CONF_INSTALL}/logs" \
  &&  chown -R bamboo:        "${CONF_INSTALL}/work" \
  &&  chmod -R 700            "${CONF_INSTALL}/conf" \
  &&  chmod -R 700            "${CONF_INSTALL}/temp" \
  &&  chmod -R 700            "${CONF_INSTALL}/logs" \
  &&  chmod -R 700            "${CONF_INSTALL}/work" 

COPY docker-entrypoint.sh /
RUN  chown bamboo: docker-entrypoint.sh \
  && chmod 700 docker-entrypoint.sh

EXPOSE 8085
VOLUME ["/var/atlassian/bamboo"]
WORKDIR ${CONF_HOME}

ENTRYPOINT ["/docker-entrypoint.sh"]