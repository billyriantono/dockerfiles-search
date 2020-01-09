# Un-official Dockerfile for installing the prerequisites for
# the Isabelle repository version. Isabelle itself is not included.
#
# This is mostly intended for automated builds, e.g., on a cloud platform.

FROM ubuntu
SHELL ["/bin/bash", "-c"]

# packages
ENV DEBIAN_FRONTEND=noninteractive
RUN apt-get -y update && \
  apt-get install -y curl less libfontconfig1 libgomp1 libwww-perl rlwrap unzip && \
  apt-get clean

# user
RUN useradd -m isabelle && (echo isabelle:isabelle | chpasswd)
USER isabelle
WORKDIR /home/isabelle
