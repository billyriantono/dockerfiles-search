############################################################
# Dockerfile to build a extract tool container image for the eBioKit
# Based on ubuntu:16.04
############################################################

# Set the base image to ubuntu:16.04
FROM ubuntu:16.04

# File Author / Maintainer
MAINTAINER Rafael Hernandez <ebiokit@gmail.com>

################## BEGIN INSTALLATION ######################

RUN apt-get update && apt-get install pbzip2

COPY configs/entrypoint.sh /usr/bin/entrypoint.sh

##################### INSTALLATION END #####################

ENTRYPOINT ["/usr/bin/entrypoint.sh"]
