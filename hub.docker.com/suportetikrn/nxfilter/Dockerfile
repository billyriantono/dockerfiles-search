FROM debian:stretch
ADD ./version.txt .
RUN apt update && \
    apt -y install openjdk-8-jre-headless curl unzip
RUN curl $(printf ' -O http://pub.nxfilter.org/nxfilter-%s.zip' $(cat version.txt)) && \
    cd / && \
    unzip $(printf 'nxfilter-%s.zip' $(cat version.txt)) -d /nxfilter && \
    rm $(printf 'nxfilter-%s.zip' $(cat version.txt)) && \
    chmod +x /nxfilter/bin/startup.sh
EXPOSE 53/udp 80 443 19001 19002 19003
CMD ["/nxfilter/bin/startup.sh","2>&1"]
