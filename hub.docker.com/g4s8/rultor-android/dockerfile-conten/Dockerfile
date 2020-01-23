FROM mysql:5.7.18

ARG BUILD_DATE
ARG VCS_REF
ARG VERSION

ADD ./resources /resources

RUN /resources/build && rm -rf resources

LABEL "maintainer"="cloudsquad@fxinnovation.com" \
      "org.label-schema.name"="mysql" \
      "org.label-schema.base-image.name"="docker.io/library/mysql" \
      "org.label-schema.base-image.version"="5.7.18" \
      "org.label-schema.description"="MySQL in a container" \
      "org.label-schema.url"="https://www.mysql.com" \
      "org.label-schema.vcs-url"="https://bitbucket.org/fxadmin/public-common-docker-mysql" \
      "org.label-schema.vendor"="FXinnovation" \
      "org.label-schema.schema-version"="1.0.0-rc.1" \
      "org.label-schema.applications.mysql.version"=$MYSQL_VERSION \
      "org.label-schema.applications.gosu.version"=$GOSU_VERSION \
      "org.label-schema.vcs-ref"=$VCS_REF \
      "org.label-schema.version"=$VERSION \
      "org.label-schema.build-date"=$BUILD_DATE \
      "org.label-schema.usage"="Should only be used on k8s. Check README.md for details why."
