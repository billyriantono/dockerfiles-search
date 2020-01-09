# Dockerfile to build picard tools
# Ref) genomicpariscentre/picard

FROM ubuntu:14.04

LABEL maintainer="Hiroki Danno <redgrapefruit@mac.com>" \
      description="A containerized Picard Tools" \
      license="https://github.com/broadinstitute/picard/blob/master/LICENSE.txt"

RUN apt-get update && \
    apt-get install --yes \
        openjdk-7-jre-headless \
        unzip \
        wget && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/ && \
    ZIP=picard-tools-1.134.zip && \
    wget https://github.com/broadinstitute/picard/releases/download/1.134/$ZIP -O /tmp/$ZIP && \
    unzip /tmp/$ZIP -d /usr/local && \
    chmod 755 /usr/local/picard-tools-* && \
    chmod +x /usr/local/picard-tools-*/picard.jar && \
    ln -s /usr/local/picard-tools-*/picard.jar /usr/local/bin/picard.jar && \
    rm /tmp/$ZIP

CMD ["/bin/bash"]
