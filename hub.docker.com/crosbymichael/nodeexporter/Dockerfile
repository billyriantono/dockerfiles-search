FROM ubuntu:18.04 as build

RUN apt-get update && apt-get upgrade -y && apt-get install -y curl

RUN curl -o node.tar.gz -SsL https://github.com/prometheus/node_exporter/releases/download/v0.16.0/node_exporter-0.16.0.linux-amd64.tar.gz
RUN tar -zxf node.tar.gz

FROM scratch
COPY --from=build /node_exporter-0.16.0.linux-amd64/node_exporter /bin/nodeexporter
