FROM sonatype/nexus3:3.16.0

MAINTAINER Mohammadreza Honarkhah <m.honar@gmail.com>

ENV SONATYPE_WORK /nexus-data

USER root

RUN chown -R nexus ${SONATYPE_WORK} && \
    chmod -R ugo+rw ${SONATYPE_WORK}

USER nexus
