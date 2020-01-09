FROM unblibraries/tomcat:7.x
MAINTAINER Jacob Sanford <jsanford_at_unb.ca>

ENV WAYBACK_URL_PREFIX http://steadfast.hil.unb.ca:8080
ENV WAYBACK_BASEDIR /data/CDX
ENV WAYBACK_WARCDIR /data/WARC

ENV OPENWAYBACK_VERSION 3.8.1
ENV MAVEN_VERSION 3.3.3
ENV JAVA_OPTS="-Djava.awt.headless=true -Xmx128M"

ENV MAVEN_ARCHIVE_FILENAME apache-maven-${MAVEN_VERSION}-bin.tar.gz
ENV MAVEN_DOWNLOAD_URL http://apache.mirror.iweb.ca/maven/maven-3/${MAVEN_VERSION}/binaries/${MAVEN_ARCHIVE_FILENAME}

ENV WAYBACK_RESOURCE_TYPE CDX

# Install required packages.
ENV DEBIAN_FRONTEND noninteractive
ENV DEBIAN_PRIORITY critical
ENV DEBCONF_NOWARNINGS yes
RUN apt-get update && \
  apt-get install -y git

# Download and set Maven in path.
WORKDIR ${APP_INSTALL_ROOT}
RUN wget ${MAVEN_DOWNLOAD_URL} && tar xvzpf ${MAVEN_ARCHIVE_FILENAME}
ENV PATH ${PATH}:${APP_INSTALL_ROOT}/apache-maven-${MAVEN_VERSION}/bin

# Clone, build OpenWayback with Maven and copy install JAR to Tomcat webapps dir.
RUN git clone https://github.com/iipc/openwayback.git openwayback
WORKDIR ${APP_INSTALL_ROOT}/openwayback
RUN mvn package && \
  rm -rf ${TOMCAT_WEBAPPS_PATH}/ROOT* && \
  mv ${APP_INSTALL_ROOT}/openwayback/wayback-webapp/target/openwayback-*-SNAPSHOT.war ${TOMCAT_WEBAPPS_PATH}/ROOT.war

# Add Conf Overrides and Images
RUN mkdir /data
ADD conf /data/conf
ADD images /data/images

# Add phusion inits.
CMD ["/sbin/my_init"]
ADD init/ /etc/my_init.d/
RUN chmod -v +x /etc/my_init.d/*.sh

# Clean up.
RUN apt-get clean && \
  rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*
