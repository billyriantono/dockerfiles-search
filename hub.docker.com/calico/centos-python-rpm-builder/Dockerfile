FROM centos:7
MAINTAINER lance@tigera.io

RUN yum install -y gcc libffi-devel git make rpm-build zlib-dev openssl-devel sqlite-devel bzip2-devel python-devel

RUN curl https://bootstrap.pypa.io/ez_setup.py | python2.7

RUN mkdir /rpms
VOLUME /rpms

ONBUILD ADD . /source
ONBUILD WORKDIR /source
# If this repo has already been built on a different architecture, the eggs may be incompatible.
ONBUILD RUN rm -rf .eggs
ONBUILD RUN python setup.py bdist_rpm

CMD ["bash", "-c", "cp -f /source/dist/*.rpm /rpms"] 
