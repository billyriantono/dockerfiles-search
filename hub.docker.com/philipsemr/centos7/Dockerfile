FROM centos:7

MAINTAINER Topology: Cristian C. Wolfram <cristian.wolfram@philips.com>, Jean Pereira <jean.pereira1@philips.com> and Junieh Byegmann <junieh.byegmann@philips.com>

LABEL name="CentOS 7 - x86_64" \
	vendor="Philips Clinical Informatics"

RUN yum update -y && \
	yum -y install bash ca-certificates chkconfig curl iproute net-tools wget && \
	yum clean all

