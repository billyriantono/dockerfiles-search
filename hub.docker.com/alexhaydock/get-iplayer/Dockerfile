FROM ubuntu:18.04
LABEL maintainer "Alex Haydock <alex@alexhaydock.co.uk>"

# Setup Environment for Ubuntu
ENV DEBIAN_FRONTEND noninteractive

RUN set -xe \
    \
# Update package list and install software-properties-common so we can use PPAs
    && apt-get update \
    && apt-get -y install software-properties-common \
    \
# Add get-iplayer official PPA
    && add-apt-repository ppa:jon-hedgerows/get-iplayer \
    \
# Update package list again
    && apt-get update \
    \
# Add the get-iplayer package
    && apt-get -y install get-iplayer \
    \
# Remove the software-properties-common package
    && apt-get -y purge software-properties-common \
    && apt-get -y autoremove \
    \
# Clear package cache to save space
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/

WORKDIR /opt/get-iplayer
ENTRYPOINT ["/usr/bin/get-iplayer"]
CMD ["--help"]
