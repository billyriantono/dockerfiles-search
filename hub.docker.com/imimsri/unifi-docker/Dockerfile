FROM debian:stretch-slim
  # WORKING: work around openjdk issue which expects the man-page directory, failing to configure package if it doesn't
# FROM debian:stretch-slim
  # needs minor fixes to get working but results in much larger image
MAINTAINER Jacob Alberty <jacob.alberty@foundigital.com>

ARG DEBIAN_FRONTEND=noninteractive

ENV PKGURL=https://dl.ubnt.com/unifi/5.5.24/unifi_sysvinit_all.deb

# Push installing openjdk-8-jre first, so that the unifi package doesn't pull in openjdk-7-jre as a dependency? Else uncomment and just go with openjdk-7.
RUN mkdir -p /usr/share/man/man1/ \
 && apt-get update \
 && apt-get install -qy --no-install-recommends \
    curl \
    dirmngr \
    gnupg \
    openjdk-8-jre-headless \
    procps \
 && echo "deb http://www.ubnt.com/downloads/unifi/debian unifi5 ubiquiti" > /etc/apt/sources.list.d/20ubiquiti.list \
 && apt-key adv --keyserver keyserver.ubuntu.com --recv C0A52C50 \
 && curl -o ./unifi.deb "${PKGURL}" \
 && apt -qy install ./unifi.deb \
 && apt-get -qy purge --auto-remove \
    dirmngr \
    gnupg \
 && rm -f ./unifi.deb \
 && rm -rf /var/lib/apt/lists/*

ENV BASEDIR=/usr/lib/unifi \
  DATADIR=/var/lib/unifi \
  RUNDIR=/var/run/unifi \
  LOGDIR=/var/log/unifi

RUN ln -s ${DATADIR} ${BASEDIR}/data \
 && ln -s ${RUNDIR} ${BASEDIR}/run \
 && ln -s ${LOGDIR} ${BASEDIR}/logs
# Can't use env var, RUN doesn't support them?

VOLUME ["${DATADIR}", "${RUNDIR}", "${LOGDIR}"]

EXPOSE 6789/tcp 8080/tcp 8443/tcp 8880/tcp 8843/tcp 3478/udp

RUN mkdir -p /usr/unifi \
     /usr/local/unifi/init.d \
     /usr/unifi/init.d
COPY docker-entrypoint.sh /usr/local/bin/
COPY docker-healthcheck.sh /usr/local/bin/
COPY functions /usr/unifi/functions
COPY import_cert /usr/unifi/init.d/
RUN chmod +x /usr/local/bin/docker-entrypoint.sh \
 && chmod +x /usr/unifi/init.d/import_cert \
 && chmod +x /usr/local/bin/docker-healthcheck.sh

WORKDIR /var/lib/unifi

HEALTHCHECK CMD /usr/local/bin/docker-healthcheck.sh || exit 1

# execute controller using JSVC like original debian package does
ENTRYPOINT ["/usr/local/bin/docker-entrypoint.sh"]

CMD ["unifi"]

# execute the conroller directly without using the service
#ENTRYPOINT ["/usr/bin/java", "-Xmx${JVM_MAX_HEAP_SIZE}", "-jar", "/usr/lib/unifi/lib/ace.jar"]
  # See issue #12 on github: probably want to consider how JSVC handled creating multiple processes, issuing the -stop instraction, etc. Not sure if the above ace.jar class gracefully handles TERM signals.
#CMD ["start"]
