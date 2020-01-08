FROM n0ts/centos

MAINTAINER Naoya Nakazawa <naoya.n@gmail.com>

RUN set -x \
    && yum install -y python-pip python-devel python-virtualenv \
    && yum clean all \
    && pip install --upgrade pip \
    && pip install jq \
    && python --version \
    && pip --version

CMD ["/bin/bash"]
