FROM hiracchi/pdf-builder:latest
MAINTAINER Toshiyuki HIRANO <hiracchi@gmail.com>

ARG BUILD_DATE
ARG VCS_REF
ARG VERSION
LABEL org.label-schema.build-date=$BUILD_DATE \
      org.label-schema.vcs-ref=$VCS_REF \
      org.label-schema.vcs-url="https://github.com/hiracchi/docker-my-devenv" \
      org.label-schema.version=$VERSION
      

# packages
RUN apt-get update \
  && apt-get install -y \
    tcsh zsh \
    vim emacs less tmux direnv \
    expect tcl8.6 \
    patch wget curl \
    flex \
    gdb electric-fence \
    zlib1g-dev libbz2-dev \
    ghostscript \
  && apt-get clean && apt-get autoclean \
  && rm -rf /var/lib/apt/lists/* 

