FROM kong:1.1-centos

LABEL description="CentOS + Kong 1.2.0 + kong-oidc plugin"

RUN yum install -y git unzip && yum clean all

RUN luarocks install kong-oidc

