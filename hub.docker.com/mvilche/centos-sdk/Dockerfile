FROM centos:7
RUN yum groupinstall "Development Tools" -y && yum install gcc wget gcc-c++ expat-devel openssl openssl-devel flex bison yajl yajl-devel curl-devel curl GeoIP-devel doxygen zlib-devel -y && yum autoremove -y && \
yum clean all && rm -rf /var/cache/yum
