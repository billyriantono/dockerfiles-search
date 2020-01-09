FROM kalilinux/kali-linux-docker

LABEL MAINTAINER="Joaquin Polo <joaquin.polo@gmail.com>"
ENV DEBIAN_FRONTEND noninteractive
RUN set -x \
    && apt-get -yqq update \
    && apt-get -yqq dist-upgrade \
    && apt-get clean
CMD ["bash"]
