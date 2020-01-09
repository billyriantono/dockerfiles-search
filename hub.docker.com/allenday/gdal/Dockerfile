FROM debian:sid

MAINTAINER Allen Day <allenday@allenday.com>

RUN echo "deb http://ftp.us.debian.org/debian/ sid main contrib non-free" >> /etc/apt/sources.list
RUN echo "deb-src http://ftp.us.debian.org/debian/ sid main" >> /etc/apt/sources.list
RUN echo "deb http://ftp.us.debian.org/debian/ testing main contrib non-free" >> /etc/apt/sources.list
RUN echo "deb-src http://ftp.us.debian.org/debian/ testing main" >> /etc/apt/sources.list

RUN echo "Package: *" >> /etc/apt/preferences
RUN echo "Pin: release a=unstable" >> /etc/apt/preferences
RUN echo "Pin-Priority: 1000" >> /etc/apt/preferences
RUN echo "Package: *" >> /etc/apt/preferences
RUN echo "Pin: release a=testing" >> /etc/apt/preferences
RUN echo "Pin-Priority: 100" >> /etc/apt/preferences

RUN apt-get -y update && apt-get -y upgrade
RUN apt-get -y install locales build-essential clang

RUN apt-get -y install gdal* libgdal*

# Externally accessible data is by default put in /data
WORKDIR /data
VOLUME ["/data"]

# Output version and capabilities by default.
CMD gdalinfo --version && gdalinfo --formats && ogrinfo --formats
