############################################################
# Dockerfile to build Buongiorno LocalDeploy container
############################################################

# Set the base image to Centos6
FROM centos:centos6

# File Author / Maintainer
MAINTAINER FalchiT FalchiT

################## BEGIN INSTALLATION ######################

RUN yum install -y wget tar git && yum -y clean all

## Versions 
ENV NGINXV=1.9.7.3 \
    OPENSV=1.0.2f

## SETUP ENV for build
WORKDIR /tmp
COPY nginx.init /root/rpmbuild/SOURCES/nginx.init
COPY ngx_openresty.spec /tmp/openresty.spec
COPY entrypoint.sh /bin/entrypoint.sh
RUN yum -y install rpmdevtools rpm-build make zlib-devel readline-devel pcre-devel gcc-c++ && \
    yum -y clean all && \
    git clone https://github.com/kvspb/nginx-auth-ldap.git && \
    mkdir -p ~/rpmbuild/{SOURCES,SPECS} && \
    wget -P ~/rpmbuild/SOURCES https://openresty.org/download/openresty-${NGINXV}.tar.gz && \
    wget https://www.openssl.org/source/openssl-${OPENSV}.tar.gz && \
    tar -zvxf openssl-${OPENSV}.tar.gz && \
    chmod +x /bin/entrypoint.sh
RUN rpmbuild --define "_OPENSV ${OPENSV}" --define "_NGINXV ${NGINXV}" -ba /tmp/openresty.spec

## Entrypoint
ENTRYPOINT ["/bin/entrypoint.sh"]
CMD ["--help"]
