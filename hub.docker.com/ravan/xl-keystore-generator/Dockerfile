FROM groovy:2.5.8-jdk8
LABEL maintainer="rnaidoo@xebialabs.com"
USER root
WORKDIR /opt/xebialabs/build
COPY resources generator.groovy
RUN mkdir -p /opt/xebialabs/output
VOLUME /opt/xebialabs/output
CMD ["groovy", "generator.groovy"]