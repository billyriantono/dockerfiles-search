FROM marthym/base:1.4.0 

ARG ANSIBLE_VERSION=2.7.8
LABEL maintainer="marthym@ght1pc9kc.fr" \
      version="2.0.0" \
      ansible.version=${ANSIBLE_VERSION}

RUN export DEBIAN_FRONTEND=noninteractive && \
    apt -y update && \ 
    apt -y install python3-pip python3-setuptools gcc python3-apt python3-dev libffi-dev libssl-dev && \
    pip3 install --upgrade pip cffi wheel setuptools && \
    pip3 install ansible==2.7.8 && \
# Cleanup install
    apt -f -y --auto-remove remove gcc python3-dev libffi-dev libssl-dev && \
    apt clean && \
    apt autoclean && \
    rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*