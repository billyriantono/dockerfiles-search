FROM fedora:20
MAINTAINER Lars Kellogg-Stedman <lars@oddbit.com>

# Because sometimes we seem to get a really crappy mirror.
RUN yum -y install \
	yum-plugin-fastestmirror \
	yum-utils \
	; yum clean all

RUN yum -y upgrade \
	; yum clean all

