#Dockerfile docker-ansible
FROM python:latest
LABEL maintainer="tlnk.fr"

ARG VERSION
ARG BUILD_DATE
ARG VCS_REF

RUN apt update -y && \
  apt install -y nano openssl iputils-ping && \
  mkdir -p /root/.ssh

RUN pip install ansible ansible-lint docker-py

WORKDIR /root/
CMD ["bash"]

LABEL org.label-schema.version=$VERSION
LABEL org.label-schema.build-date=$BUILD_DATE
LABEL org.label-schema.vcs-ref=$VCS_REF
LABEL org.label-schema.vcs-url="https://github.com/tle06/docker-ansible.git"
LABEL org.label-schema.name="docker-ansible"
LABEL org.label-schema.vendor="docker-ansible"
LABEL org.label-schema.schema-version="1.0"
