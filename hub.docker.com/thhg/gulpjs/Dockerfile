# -----------------------------------------------------------------------------
#
# Description:
#   Dockerfile to create a Gulp.js image based on node:0.12.07.
#   This image contains gulpjs 3.9.0.
#
# Authors:
#   Thiago Cangussu <thhg@tuta.io>
#
# Date:
#   2015-07-28
#
# -----------------------------------------------------------------------------

## Set the base image to scratch
FROM node:0.12.7

## File Author / Maintainer
MAINTAINER Thiago Cangussu <thhg@tuta.io>

## Install gulpjs
RUN npm install -g gulp@3.9.0

## Default command
CMD ["/bin/bash"]
