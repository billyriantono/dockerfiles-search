FROM debian:9-slim

RUN apt-get update && apt-get upgrade -y
RUN apt-get install -y \
    nmap \
    python3 \
    gawk \
    && rm -rf /var/lib/apt/lists/*

ENV TARGETS "192.168.1.0/24"
ENV OPTIONS "-sV"

RUN mkdir /inventory
COPY nmapcsv.sh index.html continuousscan.sh /inventory/

EXPOSE 1337
CMD ["./inventory/continuousscan.sh"]
