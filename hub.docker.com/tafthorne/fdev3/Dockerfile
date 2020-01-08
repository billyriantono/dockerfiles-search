# golang & OpenJFK plus a few other tools

# Put the main image together
FROM golang:1.10
LABEL \
 Description="Basic golang environment with OpenJFK and a few other tools" \
 MAINTAINER="Thomas Thorne <TafThorne@GoogleMail.com>"
USER 0
RUN \
  apt-get -y update && \
  apt-get -y install \
    clang \
    openjfx \
    unzip \
  && rm -rf /var/lib/apt/lists/*; \
  adduser builder -uid 1000 --disabled-password --gecos "Bob Builder,1,2,3"; \
  echo "builder:.builder" chpasswd
USER builder

