#FROM kong:1.1.2-centos
FROM kong
LABEL maintainer="tlnk.fr"

ARG VERSION
ARG BUILD_DATE
ARG VCS_REF

#RUN yum install -y git unzip && yum clean all
RUN luarocks install kong-oidc

LABEL org.label-schema.version=$VERSION
LABEL org.label-schema.build-date=$BUILD_DATE
LABEL org.label-schema.vcs-ref=$VCS_REF
LABEL org.label-schema.vcs-url="https://github.com/tle06/kong-oidc.git"
LABEL org.label-schema.name="kong-oidc"
LABEL org.label-schema.vendor="kong-oidc"
LABEL org.label-schema.schema-version="1.1.2-centos"