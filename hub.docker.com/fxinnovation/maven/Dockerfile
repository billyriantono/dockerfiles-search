FROM maven:3.3-jdk-8

ENV NPM_VERSION=1.4.21+ds-2 \
    XVFB_VERSION=2.1.16.4-1 \
    CHROMIUM_VERSION=57.0.2987.98-1~deb8u1

ARG BUILD_DATE
ARG VCS_REF
ARG VERSION

ADD ./resources /resources

RUN /resources/build && rm -rf resources

LABEL "maintainer"="cloudsquad@fxinnovation.com" \
      "org.label-schema.name"="maven" \
      "org.label-schema.base-image.name"="docker.io/library/maven" \
      "org.label-schema.base-image.version"="3.3-jdk-8" \
      "org.label-schema.description"="Jenkins in a container" \
      "org.label-schema.url"="https://maven.apache.org/" \
      "org.label-schema.vcs-url"="https://bitbucket.org/fxadmin/public-common-docker-maven" \
      "org.label-schema.vendor"="FXinnovation" \
      "org.label-schema.schema-version"="1.0.0-rc.1" \
      "org.label-schema.applications.java.version"=$JAVA_VERSION \
      "org.label-schema.applications.maven.version"=$MAVEN_VERSION \
      "org.label-schema.applications.ca-certificates-java.version"=$CA_CERTIFICATES_JAVA_VERSION \
      "org.label-schema.applications.npm.version"=$NPM_VERSION \
      "org.label-schema.applications.xvfb.version"=$XVFB_VERSION \
      "org.label-schema.applications.chromium.version"=$CHROMIUM_VERSION \
      "org.label-schema.vcs-ref"=$VCS_REF \
      "org.label-schema.version"=$VERSION \
      "org.label-schema.build-date"=$BUILD_DATE \
      "org.label-schema.usage"="Noob"
