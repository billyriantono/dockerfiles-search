FROM ubuntu:latest
MAINTAINER UKAEA <admin@fispact.ukaea.uk>

# Build-time metadata as defined at http://label-schema.org
ARG PROJECT_NAME
ARG BUILD_DATE
ARG VCS_REF
ARG VERSION
LABEL org.label-schema.build-date=$BUILD_DATE \
      org.label-schema.name="$PROJECT_NAME" \
      org.label-schema.description="Ubuntu docker image with TeX Live" \
      org.label-schema.url="" \
      org.label-schema.vcs-ref=$VCS_REF \
      org.label-schema.vcs-url="https://github.com/fispact/docker_texlive" \
      org.label-schema.vendor="UKAEA" \
      org.label-schema.version=$VERSION \
      org.label-schema.license="Apache-2.0" \
      org.label-schema.schema-version="1.0"

# Install additional packages
RUN apt-get --yes update && \
    apt-get --yes upgrade && \
    apt-get --yes install sudo && \
    DEBIAN_FRONTEND=noninteractive && \
    apt-get install -y tzdata && \
    apt-get --yes install texlive texlive-latex-recommended texlive-latex-extra texlive-publishers texlive-font-utils && \
    apt-get --yes install git ssh gnuplot

