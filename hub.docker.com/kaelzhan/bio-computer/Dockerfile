FROM cardcorp/r-java:latest
MAINTAINER kael.zhan@qq.com

COPY provision/* /opt/provision/

#
# The Debian release referenced below for the Mesosphere repo should be
# compatible with the one used by the upstream Jenkins container.
#
RUN cd /opt/provision \
    && ./base-setup.sh \
    && ./install-packages.sh \
    && ./base-cleanup.sh

# ADD and COPY are always done as root regardless of the USER directive preceeding them so
# chown the plugins copied over above