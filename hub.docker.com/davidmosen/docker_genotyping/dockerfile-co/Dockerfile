FROM debian:jessie

RUN apt-get update && \
    apt-get install -y varnish \
                    --no-install-recommends && rm -r /var/lib/apt/lists/*

ENV VARNISH_PORT 6081

EXPOSE 6081

COPY start /usr/local/bin/start

RUN chmod +x /usr/local/bin/start

CMD ["start"]
