# Based on nginx image
FROM robomod/nginx:0.1.1
MAINTAINER Andreas Ihrig (RoboMod) <mod.andy@gmx.de>

# Use passenger-docker approach and scripts
ENV HOME /root
ADD . /build
RUN /build/scripts/install.sh