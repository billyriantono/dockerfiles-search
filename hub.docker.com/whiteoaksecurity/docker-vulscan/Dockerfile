FROM alpine:latest
MAINTAINER Christopher Emerson <christopher.emerson@whiteoaksecurity.com>

RUN apk --update add nmap nmap-scripts && rm -f /var/cache/apk/*

RUN apk add --update wget && rm -rf /var/cache/apk/*

RUN wget http://www.computec.ch/projekte/vulscan/download/nmap_nse_vulscan-2.0.tar.gz && tar -xvzf nmap_nse_vulscan-2.0.tar.gz -C /usr/share/nmap/scripts/

WORKDIR /usr/share/nmap/scripts/vulscan
#RUN wget --no-check-certificate https://raw.githubusercontent.com/offensive-security/exploit-database/master/files.csv -o exploitdb.csv
#RUN wget --no-check-certificate http://cve.mitre.org/data/downloads/allitems.csv -o cve.csv

RUN mkdir /nmap
VOLUME ["/nmap"]
WORKDIR /nmap

ENTRYPOINT ["nmap"]
