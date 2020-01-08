FROM debian:jessie
MAINTAINER Cem Ozer <cemoezer@gmail.com>

ARG DEBIAN_FRONTEND=noninteractive

ADD docker/data/setup_dirs.sh /opt/sfm-setup/

CMD sh /opt/sfm-setup/setup_dirs.sh