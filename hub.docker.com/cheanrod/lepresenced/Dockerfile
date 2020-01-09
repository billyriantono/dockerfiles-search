FROM debian:buster-slim

ENV DEBIAN_FRONTEND noninteractive
ENV TERM xterm

RUN apt-get update && apt-get -qqy --no-install-recommends install \
    perl \
    libnet-server-perl \
    libusb-1.0-0-dev \
    bluetooth \
    bluez \
    blueman \
    tzdata \
    bluez-hcidump && \
    apt-get clean && cd / && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

WORKDIR /opt

ADD https://svn.fhem.de/fhem/trunk/fhem/contrib/PRESENCE/lepresenced lepresenced
RUN chmod +x lepresenced && \
    chgrp -cR dialout lepresenced

EXPOSE 5333

CMD /usr/bin/perl /opt/lepresenced --device "hci0" --listenaddress "0.0.0.0" --listenport 5333 --loglevel "LOG_WARNING" --logtarget stdout
