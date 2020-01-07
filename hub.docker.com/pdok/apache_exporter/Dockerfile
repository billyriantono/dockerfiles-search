from debian:buster-slim

COPY apache_exporter-0.6.0.linux-amd64/apache_exporter /apache_exporter

RUN chmod +rwx /apache_exporter

EXPOSE 9117
ENTRYPOINT ["/apache_exporter"]