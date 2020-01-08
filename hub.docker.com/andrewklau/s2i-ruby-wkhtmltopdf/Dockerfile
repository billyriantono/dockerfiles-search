FROM quay.io/ausnimbus/s2i-ruby-scl:2.2

USER 0

RUN yum install -y --setopt=tsflags=nodocs urw-fonts libXext libXrender \
    fontconfig libfontconfig.so.1 xorg-x11-fonts-Type1 xorg-x11-fonts-75dpi libjpeg-turbo \
    libX11 libXext libXrender libpng && \
    yum install -y http://download.gna.org/wkhtmltopdf/0.12/0.12.2.1/wkhtmltox-0.12.2.1_linux-centos7-amd64.rpm && \
    yum clean all -y

USER 1001
