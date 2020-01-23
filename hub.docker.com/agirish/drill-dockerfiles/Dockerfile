FROM centos:7

# Project version defined in pom.xml is passed as an argument
ARG VERSION=1.16.0
ARG MIRROR=http://mirrors.ibiblio.org

EXPOSE 8047 31010 31011 31012

# JDK 8 is a pre-requisite to run Drill ; 'which' package is needed for drill-config.sh
RUN yum install -y java-1.8.0-openjdk-devel vim which stress wget ; yum clean all ; rm -rf /var/cache/yum

# Download Drill $VERSION Tarball
RUN wget $MIRROR/apache/drill/drill-$VERSION/apache-drill-$VERSION.tar.gz >/dev/null 2>&1

# The drill tarball is generated upon building the Drill project
RUN cp apache-drill-$VERSION.tar.gz /tmp

# Drill binaries are extracted into the '/opt/drill' directory
RUN mkdir /opt/drill
RUN tar -xvzf /tmp/apache-drill-$VERSION.tar.gz --directory=/opt/drill --strip-components 1

# Copy configurations & scripts into Docker container
COPY drill-env.sh drill-override.conf /opt/drill/conf/
COPY start.sh drill-status.sh drill-graceful-stop.sh /opt/drill/bin/
RUN chmod +x /opt/drill/conf/drill-env.sh && \
    chmod +x /opt/drill/bin/start.sh && \
    chmod +x /opt/drill/bin/drill-status.sh && \
    chmod +x /opt/drill/bin/drill-graceful-stop.sh

# Starts Drill
CMD ["/bin/bash", "-c", "/opt/drill/bin/start.sh"]