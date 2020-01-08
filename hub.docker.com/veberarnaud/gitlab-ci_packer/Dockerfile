FROM alpine:3.6
MAINTAINER "VEBER Arnaud <https://github.com/VEBERArnaud>"
#
# install bash & make
RUN apk --update add bash make

# packer version to install
ENV PACKER_VERSION=1.0.2

# download packer zip
ADD https://releases.hashicorp.com/packer/${PACKER_VERSION}/packer_${PACKER_VERSION}_linux_amd64.zip ./

# install packer
RUN unzip packer_${PACKER_VERSION}_linux_amd64.zip -d /bin
RUN rm -f packer_${PACKER_VERSION}_linux_amd64.zip
