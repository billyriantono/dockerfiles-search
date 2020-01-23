FROM alpine:3.3

MAINTAINER Frederik Granna

RUN apk add --update git cmake build-base libusb-dev bash && \
    rm -rf /var/cache/apk/*

WORKDIR /tmp

RUN echo 'blacklist dvb_usb_rtl28xxu' > /etc/modprobe.d/raspi-blacklist.conf && \
    git clone git://git.osmocom.org/rtl-sdr.git && \
    mkdir rtl-sdr/build && \
    cd rtl-sdr/build && \
    cmake ../ -DINSTALL_UDEV_RULES=ON -DDETACH_KERNEL_DRIVER=ON && \
    make  && \
    make install && \
    cd .. && \
    rm -rf /tmp/rtl-sdr

ENTRYPOINT ["bash"]
