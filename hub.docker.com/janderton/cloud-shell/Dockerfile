FROM phusion/baseimage:0.10.1

LABEL maintainer="James Anderton <janderton@burwood.com>"
LABEL description="A Python 3 enabled Multi-Cloud Shell with aws/azure/google sdk's and cli's installed"

ENV CREDENTIAL_FILE=~/.aws/credentials

COPY . /app/
WORKDIR /app/

#Installing required packages and changing /usr/bin/python softlink to point to python3 as its needed for the aws scripts to run
#Then cleaning up the cache and removing unneeded dev libs
RUN export CLOUD_SDK_REPO="cloud-sdk-$(lsb_release -c -s)" && \
    echo "deb http://packages.cloud.google.com/apt $CLOUD_SDK_REPO main" | \
    tee -a /etc/apt/sources.list.d/google-cloud-sdk.list && \
    curl https://packages.cloud.google.com/apt/doc/apt-key.gpg | apt-key add - && \
    apt update && \
    apt install curl git gcc make python3 python3-pip jq python3-dev python-configobj musl-dev libffi-dev libssl-dev -y && \
    rm -rf /usr/bin/python && \
    ln -s /usr/bin/python3 /usr/bin/python && \
    pip3 install -r requirements.txt && \
    apt install google-cloud-sdk -y && \
    apt-get remove gcc make python3-dev musl-dev libffi-dev libssl-dev -y && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

# Use baseimage-docker's init system.
CMD ["/sbin/my_init"]
