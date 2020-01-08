FROM ubuntu:16.04

ARG ANSIBLE_VERSION=2.3.0.0
ENV HOME=/tmp

RUN set -x \
    && apt-get update -qq \
    && apt-get install -y -qq --no-install-recommends \
      build-essential \
      ca-certificates \
      libffi6 \
      libffi-dev \
      libssl1.0.0 \
      libssl-dev \
      openssh-client \
      python-dev \
      python-pip \
      python-setuptools \
      sshpass \
    && pip install wheel \
    && pip install \
      ansible==$ANSIBLE_VERSION \
      docker-py \
      pywinrm \
    && apt-get purge -q -y --auto-remove \
      build-essential \
      libffi-dev \
      libssl-dev \
    && apt-get clean -q \
    && rm -rf /var/lib/apt/lists/* \
    && mkdir /ansible

VOLUME ["/ansible"]
WORKDIR /ansible

ENTRYPOINT ["ansible-playbook"]
CMD ["playbooks/site.yml"]
