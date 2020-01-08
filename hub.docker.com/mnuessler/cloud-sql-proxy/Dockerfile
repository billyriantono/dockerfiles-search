FROM ubuntu:xenial

MAINTAINER Matthias Nuessler <m.nuessler@web.de>

ADD https://dl.google.com/cloudsql/cloud_sql_proxy.linux.amd64 /usr/local/bin/cloud_sql_proxy
RUN chmod +x /usr/local/bin/cloud_sql_proxy

EXPOSE 3306

CMD ["--help"]
ENTRYPOINT ["/usr/local/bin/cloud_sql_proxy", "-dir=/cloudsql"]
