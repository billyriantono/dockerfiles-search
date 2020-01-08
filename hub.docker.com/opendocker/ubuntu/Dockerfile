#
# Ubuntu base image
#
# https://github.com/opendocker/ubuntu
#

# phusion baseimage!
FROM phusion/baseimage:0.9.12

# Add our build directory
RUN mkdir /build
ADD . /build

# Run our stuff
RUN \
	/build/install.sh && \
	/build/cleanup.sh

# Run python by default
CMD ["/sbin/my_init", "--", "/bin/bash"]
