FROM opensuse:13.2
MAINTAINER Jeff Bonhag <jbonhag@sca-corp.com>

RUN zypper --gpg-auto-import-keys ref
RUN zypper --non-interactive in curl unzip java-1_7_0-openjdk

RUN curl -OL http://sourceforge.net/projects/geoserver/files/GeoServer/2.6.0/geoserver-2.6.0-bin.zip \
  && unzip geoserver-2.6.0-bin.zip && rm geoserver-2.6.0-bin.zip

EXPOSE 8080
CMD ["./geoserver-2.6.0/bin/startup.sh"]

