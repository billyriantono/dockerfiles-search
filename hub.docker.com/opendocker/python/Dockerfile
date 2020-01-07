#
# Python image
#
# https://github.com/opendocker/python
#

# ubuntu base
FROM opendocker/ubuntu:0.2.0

# Add our build directory
RUN mkdir /build
ADD . /build

# Run our stuff
RUN \
	/build/install.sh && \
	/build/cleanup.sh

CMD ["/sbin/my_init", "--", "/usr/bin/python"]
