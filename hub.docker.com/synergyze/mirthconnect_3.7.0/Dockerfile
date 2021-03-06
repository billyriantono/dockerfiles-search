FROM openjdk 
ENV MIRTH_CONNECT_VERSION 3.7.0.b2399 
RUN useradd -u 1000 mirth
# To work around the gpg: cannot open '/dev/tty': No such device or address issue: https://github.com/nodejs/docker-node/issues/922
RUN gpg --no-tty --keyserver pool.sks-keyservers.net --recv-keys B42F6819007F00F88E364FD4036A9C25BF357DD4
RUN apt-get update && apt-get install -y --no-install-recommends ca-certificates wget && rm -rf /var/lib/apt/lists/* \
	&& wget -O /usr/local/bin/gosu "https://github.com/tianon/gosu/releases/download/1.2/gosu-$(dpkg --print-architecture)" \
	&& wget -O /usr/local/bin/gosu.asc "https://github.com/tianon/gosu/releases/download/1.2/gosu-$(dpkg --print-architecture).asc" \
	&& gpg --verify /usr/local/bin/gosu.asc \
	&& rm /usr/local/bin/gosu.asc \
	&& chmod +x /usr/local/bin/gosu
VOLUME /opt/mirth-connect/appdata
RUN \
  cd /tmp && \
  wget http://downloads.mirthcorp.com/connect/$MIRTH_CONNECT_VERSION/mirthconnect-$MIRTH_CONNECT_VERSION-unix.tar.gz && \
  tar xvzf mirthconnect-$MIRTH_CONNECT_VERSION-unix.tar.gz && \
  rm -f mirthconnect-$MIRTH_CONNECT_VERSION-unix.tar.gz && \
  mv Mirth\ Connect/* /opt/mirth-connect/ && \
  chown -R mirth /opt/mirth-connect
COPY mirth.properties /tmp
COPY extension.properties /tmp
RUN \
  cp -af /tmp/mirth.properties /opt/mirth-connect/conf/ && \
  cp -af /tmp/extension.properties /opt/mirth-connect/appdata/
WORKDIR /opt/mirth-connect
EXPOSE 8080 8443
COPY docker-entrypoint.sh /
RUN chmod a+x /docker-entrypoint.sh
ENTRYPOINT ["/docker-entrypoint.sh"]
CMD ["java", "-jar", "mirth-server-launcher.jar"]