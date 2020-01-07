FROM    httpd:2.4

MAINTAINER Robert Gusick "robert@gusick.com"

ARG     DEBIAN_FRONTEND=noninteractive

RUN     apt-get update && \
        apt-get install -y --no-install-recommends \
        libcgi-pm-perl \
        libemail-mime-perl \
        libemail-sender-perl \
        libmime-lite-perl \
        libimage-magick-perl \
        mailutils \
        dma
