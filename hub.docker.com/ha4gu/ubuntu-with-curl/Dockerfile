FROM ubuntu:18.04
ENV DEBCONF_NOWARNINGS yes
RUN  apt-get update -qq \
  && apt-get install -qq -y --no-install-recommends \
    curl \
    ca-certificates \
  && apt-get clean \
  && rm -rf /var/lib/apt/lists/*
