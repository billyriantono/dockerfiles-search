FROM openjdk:8-jdk-alpine
MAINTAINER Jochen Schalanda <jochen+docker@schalanda.name>

ENV JAPI_COMPLIANCE_CHECKER_VERSION 2.4
ENV JAPI_MONITOR_VERSION 1.3
ENV JAPI_TRACKER_VERSION 1.3
ENV PKGDIFF_VERSION 1.7.2

# Build-time metadata as defined at http://label-schema.org
ARG VCS_REF
ARG VERSION

LABEL org.label-schema.name="Java API Tracker Docker images" \
      org.label-schema.description="Java API Tracker Docker image based on Alpine Linux" \
      org.label-schema.url="https://lvc.github.io/japi-tracker/" \
      org.label-schema.vcs-ref=$VCS_REF \
      org.label-schema.vcs-url="https://github.com/joschi/docker-japi-tracker" \
      org.label-schema.version=$VERSION \
      org.label-schema.schema-version="1.0" \
      com.microscaling.docker.dockerfile="/Dockerfile" \
      com.microscaling.license="MIT"

VOLUME /workspace
WORKDIR /workspace

RUN apk add --no-cache binutils curl make perl gnuplot file
RUN \
  wget -q -O - "https://github.com/lvc/japi-compliance-checker/archive/${JAPI_COMPLIANCE_CHECKER_VERSION}.tar.gz" | tar -C /tmp -xzf - && \
  cd "/tmp/japi-compliance-checker-${JAPI_COMPLIANCE_CHECKER_VERSION}" && \
  make install && \
  rm -rf "/tmp/japi-compliance-checker-${JAPI_COMPLIANCE_CHECKER_VERSION}"
RUN \
  wget -q -O - "https://github.com/lvc/japi-monitor/archive/${JAPI_MONITOR_VERSION}.tar.gz" | tar -C /tmp -xzf - && \
  cd "/tmp/japi-monitor-${JAPI_MONITOR_VERSION}" && \
  make install && \
  rm -rf "/tmp/japi-monitor-${JAPI_MONITOR_VERSION}"
RUN \
  wget -q -O - "https://github.com/lvc/pkgdiff/archive/${PKGDIFF_VERSION}.tar.gz" | tar -C /tmp -xzf - && \
  cd "/tmp/pkgdiff-${PKGDIFF_VERSION}" && \
  make install && \
  rm -rf "/tmp/pkgdiff-${PKGDIFF_VERSION}"
RUN \
  wget -q -O - "https://github.com/lvc/japi-tracker/archive/${JAPI_TRACKER_VERSION}.tar.gz" | tar -C /tmp -xzf - && \
  cd "/tmp/japi-tracker-${JAPI_TRACKER_VERSION}" && \
  make install && \
  rm -rf "/tmp/japi-tracker-${JAPI_TRACKER_VERSION}"

#ENTRYPOINT ["japi-tracker"]
