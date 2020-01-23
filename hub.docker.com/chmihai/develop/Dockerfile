FROM debian:buster-slim
LABEL description="Home-Assistant"

RUN apt-get update && apt-get install -y nano tcpdump net-tools openvpn usbip curl python3-pip libssl-dev libffi-dev python3-dev \
        inetutils-ping dbus libudev-dev libavformat-dev libavcodec-dev libavdevice-dev libavutil-dev  libswscale-dev libswresample-dev \
        libavfilter-dev python3-setuptools \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/*
RUN /usr/bin/python3 -m pip install homeassistant aiohttp_cors==0.7.0 gTTS-token==1.1.3 PyNaCl==1.3.0 hass-nabucasa==0.17 mutagen==1.42.0 distro==1.4.0 netdisco==2.6.0 sqlalchemy==1.3.7 aiohttp_cors==0.7.0 pyotp==2.2.7 PyQRCode==1.2.1 home-assistant-frontend==20190828.1
ENV SHELL /bin/bash
RUN mkdir /config -p
RUN curl https://www.virtualhere.com/sites/default/files/usbclient/vhclientx86_64 -o /usr/bin/vhclient
RUN chmod +x /usr/bin/vhclient
CMD ["/usr/bin/vhclient", "-n"]
CMD ["/usr/bin/vhclient", "-t", "AUTO USE HUB,172.16.0.30"]
CMD ["/usr/bin/python3", "-m",  "homeassistant", "-c", "/config"]
