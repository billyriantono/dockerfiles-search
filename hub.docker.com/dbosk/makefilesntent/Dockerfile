ARG BASE_IMAGE=debian:stretch-slim
FROM ${BASE_IMAGE}
ARG WORD=default
ENV AWORD=${WORD}
CMD cat /etc/lsb-release || cat /etc/debian_version || true
