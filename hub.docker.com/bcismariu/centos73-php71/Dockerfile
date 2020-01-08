FROM centos:7.3.1611
MAINTAINER Bogdan Cismariu <bogdan.cismariu@gmail.com>

# Copying helper files
ADD *.sh ./
RUN chmod +x *.sh

RUN ./install-php71.sh

RUN ./install-utils.sh

