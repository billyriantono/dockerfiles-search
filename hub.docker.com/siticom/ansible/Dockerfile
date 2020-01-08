FROM alpine:3.9

ARG ansible_version=2.7.0-r1

LABEL maintainer="Lukas Steiner <lukas.steiner@siticom.de>"
LABEL ansible_version="$ansible_version"

RUN apk --no-cache add bash openssh ansible=${ansible_version}

COPY ansible.cfg /etc/ansible/ansible.cfg
