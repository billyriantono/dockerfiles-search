FROM java:7u79-jdk
MAINTAINER Colin Woodcock "colin.woodcock@gmail.com"

ENV SMIX_VERSION 6.0.0
ENV JAVA_HOME /usr/lib/jvm/java-7-openjdk-amd64

# Fetch
RUN wget http://mirrors.ukfast.co.uk/sites/ftp.apache.org/servicemix/servicemix-6/${SMIX_VERSION}/apache-servicemix-${SMIX_VERSION}.zip;

# Explode and configure
RUN \
  unzip -d /opt apache-servicemix-${SMIX_VERSION}.zip && \
  rm -f apache-servicemix-${SMIX_VERSION}.zip && \
  ln -s /opt/apache-servicemix-${SMIX_VERSION} /opt/servicemix && \
  useradd -r servicemix -d /opt/servicemix && \
  chown -R servicemix:servicemix /opt/apache-servicemix-${SMIX_VERSION}

VOLUME ["/opt/servicemix/deploy"]
VOLUME ["/opt/servicemix/data"]

EXPOSE 1099 5505 8101 44444 61616

USER servicemix
ENTRYPOINT ["/opt/servicemix/bin/servicemix"]
CMD ["start"]
