
FROM alpine:latest

RUN apk add --no-cache curl

RUN curl -LO https://github.com/Lusitaniae/apache_exporter/releases/download/v0.7.0/apache_exporter-0.7.0.linux-amd64.tar.gz; \
tar xvf apache_exporter-0.7.0.linux-amd64.tar.gz; \
cp apache_exporter-0.7.0.linux-amd64/apache_exporter /usr/local/bin/apache_exporter; \
rm -rf  apache_exporter-0.7.0.linux-amd64*

EXPOSE 9117
CMD ["/usr/local/bin/apache_exporter", "--scrape_uri=http://localhost:8081/server-status?auto", ">", "/dev/null"]
