# PixelHyperlink DataCenterServer Docker
#
# VERSION               1.0.0

FROM pixelhyperlinkdockers/ubuntu:latest
MAINTAINER Abhishek Salian <abhi@pixelhyperlink.com>

LABEL Description="This image contains base ubuntu os for data storage."
LABEL Vendor="PixelHyperlink"
LABEL Version="1.0.0"

# Copy server start up scripts
ADD ./startup.sh /opt/startup.sh

# Create directory for storage
RUN mkdir /usr/storage

# Copy this repo into place.
ADD ./data_storage/data /usr/storage

VOLUME /usr/storage

# Run startup scripts
CMD ["/bin/bash", "/opt/startup.sh"]