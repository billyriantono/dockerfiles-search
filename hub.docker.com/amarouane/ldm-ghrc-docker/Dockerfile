FROM unidata/ldm-docker:6.13.7

RUN yum install -y centos-release-scl && \
    yum install -y rh-python36

ENV PATH=/opt/rh/rh-python36/root/usr/bin:$PATH

RUN pip install awscli
