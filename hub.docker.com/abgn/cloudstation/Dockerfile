FROM ubuntu:latest

ENV DEBIAN_FRONTEND noninteractive
RUN apt-get update
RUN apt-get install -y wget libqt5widgets5 libqt5Network5 supervisor
RUN mkdir -p /var/log/supervisor
RUN wget http://global.download.synology.com/download/Tools/CloudStation/3482/Ubuntu/x64/synology-cloud-station-3482.deb -O /usr/src/synology.deb
RUN dpkg -i /usr/src/synology.deb || true
RUN apt-get install -fy	

COPY supervisord.conf /etc/supervisor/conf.d/supervisord.conf
RUN localedef -v -c -i en_US -f UTF-8 en_US.UTF-8 || true
RUN echo "Europe/Stockholm" > /etc/timezone
RUN dpkg-reconfigure tzdata

ENV LD_LIBRARY_PATH=/opt/Synology/CloudStation/lib
ENTRYPOINT ["/usr/bin/supervisord"]
