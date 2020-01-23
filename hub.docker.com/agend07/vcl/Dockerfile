FROM debian:wheezy

RUN apt-get update
RUN apt-get install -y libgeoip1 curl

RUN curl -o GeoIP.dat.gz http://geolite.maxmind.com/download/geoip/database/GeoLiteCountry/GeoIP.dat.gz
RUN gzip -d GeoIP.dat.gz

ENTRYPOINT ["/vcl"]




