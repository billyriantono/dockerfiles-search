FROM openjdk:8u151

# install libltdl.so.7
RUN set -eux; \
  apt-get update && \
  apt-get install libltdl7 -y && \
  rm -rf /var/lib/apt/lists/*
