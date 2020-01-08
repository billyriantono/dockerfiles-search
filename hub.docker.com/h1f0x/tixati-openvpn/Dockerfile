# NOTE: glibc version of the image is needed for the 7-Zip-JBinding workaround.
FROM jlesage/baseimage-gui:debian-9

RUN apt-get update

RUN apt-get install -y apt-utils sudo

RUN apt-get install -y xterm bash curl wget iptables openvpn procps

RUN apt-get install -y dbus ibgtk2.0-0 libdbus-glib-1-2

# Maximize only the main/initial window.
RUN \
    sed-patch 's/<application type="normal">/<application type="normal" title="Tixati">/' \
        /etc/xdg/openbox/rc.xml

VOLUME ["/output"]
VOLUME ["/config"]
VOLUME ["/vpn"]

# Add files.
COPY rootfs/ /

# Set environment variables.
ENV APP_NAME="Tixati" \
    S6_KILL_GRACETIME=8000

RUN \
    APP_ICON_URL=https://raw.githubusercontent.com/h1f0x/tixati-openvpn/master/images/tixati.png && \
    install_app_icon.sh "$APP_ICON_URL"

RUN useradd --create-home app

RUN ln -s /config/.tixati /home/app/

# Metadata.
LABEL \
      org.label-schema.name="tixati" \
      org.label-schema.description="Docker container for Tixati" \
      org.label-schema.version="unknown" \