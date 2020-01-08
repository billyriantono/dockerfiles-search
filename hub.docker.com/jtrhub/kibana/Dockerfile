FROM jtrhub/debian-wheezy

RUN mkdir /kibana \
    && curl "https://download.elastic.co/kibana/kibana/kibana-4.1.0-linux-x64.tar.gz" | tar xz -C /kibana --strip=1

EXPOSE 5601

CMD ["/kibana/bin/kibana"]
