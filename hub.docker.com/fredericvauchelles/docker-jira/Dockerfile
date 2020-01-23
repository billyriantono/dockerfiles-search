FROM debian:latest

# Setup useful environment variables
ENV CONF_HOME             /var/atlassian/jira
ENV CONF_INSTALL          /opt/atlassian/jira
ENV CONF_VERSION          7.2.1
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
RUN   groupadd -r jira --gid=999 \
   && useradd -r -g jira --uid=999 jira

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

# Create jira directories
RUN   mkdir -p                "${CONF_HOME}" \
  &&  chown -R jira:          "${CONF_HOME}" \
  &&  chmod -R 700            "${CONF_HOME}" \
  &&  mkdir -p                "${CONF_INSTALL}/conf"

# Download and install jira
RUN   curl -Ls                "https://downloads.atlassian.com/software/jira/downloads/atlassian-jira-software-${CONF_VERSION}.tar.gz" \
  |   tar -xz --directory "${CONF_INSTALL}" --strip-components=1 --no-same-owner 

# Setup configuration
RUN  echo                 "jira.home=$CONF_HOME" > "${CONF_INSTALL}/atlassian-jira/WEB-INF/classes/jira-application.properties" 

# Setup permissions
RUN   chown -R jira:    "${CONF_INSTALL}/temp" \
  &&  chown -R jira:    "${CONF_INSTALL}/logs" \
  &&  chown -R jira:    "${CONF_INSTALL}/work" \
  &&  chown -R jira:    "${CONF_INSTALL}/conf" \
  &&  chmod -R 700      "${CONF_INSTALL}/temp" \
  &&  chmod -R 700      "${CONF_INSTALL}/logs" \
  &&  chmod -R 700      "${CONF_INSTALL}/work" \
  &&  chmod -R 700      "${CONF_INSTALL}/conf"

COPY docker-entrypoint.sh /
RUN  chown jira: docker-entrypoint.sh \
  && chmod 700 docker-entrypoint.sh

EXPOSE 8080
VOLUME ["/var/atlassian/jira"]
WORKDIR ${CONF_HOME}

ENTRYPOINT ["/docker-entrypoint.sh"]