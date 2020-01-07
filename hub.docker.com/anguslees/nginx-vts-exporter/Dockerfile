FROM alpine:3.4
MAINTAINER Angus Lees <gus@inodes.org>

ADD nginx-vts-exporter-linux-amd64.tar.gz /usr/local/bin/
RUN chmod +x /usr/local/bin/nginx-vts-exporter

EXPOSE 9913
CMD ["nginx-vts-exporter"]
