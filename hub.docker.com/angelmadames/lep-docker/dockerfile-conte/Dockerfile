FROM andzuc/gentoo-tc:avr

RUN echo "USE='-gtk -alsa -cups -webstart'" >>/etc/portage/make.conf

RUN time emerge -v \
    --autounmask-write=y \
    --autounmask-continue=y \
    dev-java/icedtea-bin
RUN time emerge -v \
    --autounmask-write=y \
    --autounmask-continue=y \
    dev-embedded/arduino

RUN useradd -m arduino
USER arduino
ENV HOME /home/ardiono
WORKDIR /home/arduino
ENTRYPOINT ["/usr/bin/arduino"]
