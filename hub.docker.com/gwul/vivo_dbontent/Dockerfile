FROM gvgramazio/texlive:base

LABEL mantainer="gvgramazio@gmail.com" \
      version="0.1"

ARG DEBIAN_FRONTEND=noninteractive

# Install texlive-full
RUN apt-get update \
  && apt-get install -y --no-install-recommends \
    texlive-full=2017.20180305-1 \
  && apt-get clean \
  && rm -rf /var/lib/apt/lists/*

# Remove documentation packages of latex to save disk space
RUN apt-get remove -y "texlive-*-doc"
