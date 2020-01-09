FROM registry.access.redhat.com/ubi8/ubi-minimal

ENV JAVA_MAJOR_VERSION=8 \
    JAVA_HOME=/usr/lib/jvm/jre-1.8.0

RUN microdnf install java-1.8.0-openjdk-headless \
  && microdnf clean all
