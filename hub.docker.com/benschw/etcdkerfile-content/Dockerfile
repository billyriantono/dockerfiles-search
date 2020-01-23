FROM i386/debian:stable-slim


LABEL maintainer="Marcel Huber <marcelhuberfoo@gmail.com>"
EXPOSE 631
ENV EMAIL="Marcel <me@labs.com>"
COPY printer.deb /tmp/printer.deb
RUN export DEBIAN_FRONTEND noninteractive && apt update && \
    apt install -y --no-install-recommends vim git etckeeper && \
    apt install -y --no-install-recommends cups a2ps printer-driver-gutenprint foomatic-db openprinting-ppds fonts-linuxlibertine && \
    apt install -y --no-install-recommends curl python-pip python-cups python-setuptools python-wheel && \
    pip install cloudprint[daemon] && \
    sed -r -i 's/(Order allow\,deny)/\1\n  Allow all/' /etc/cups/cupsd.conf && \
    printf "DefaultEncryption Never\nServerAlias *\n" >> /etc/cups/cupsd.conf && \
    # dpkg --add-architecture i386 && \
    # apt update && apt install -y libc6:i386 && \
    cd /tmp && curl -sSL --remote-name http://download.brother.com/welcome/dlf006526/mfc9970cdwlpr-1.1.1-5.i386.deb && \
    curl -sSL --remote-name http://download.brother.com/welcome/dlf006528/mfc9970cdwcupswrapper-1.1.1-5.i386.deb && \
    mkdir -p /var/spool/lpd && dpkg -i --force-all mfc9970cdwlpr-1.1.1-5.i386.deb && \
    dpkg -i --force-all mfc9970cdwcupswrapper-1.1.1-5.i386.deb && \
    # apt install libcups2:i386 -y &&   \
    dpkg -i printer.deb && \
    rm -f /tmp/*.deb
COPY configure.sh /usr/bin/configure
COPY daemon.sh /usr/bin/daemon
VOLUME ["/root"]
CMD ["daemon"]
