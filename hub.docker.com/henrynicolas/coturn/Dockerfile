FROM debian:buster-slim

ARG DEBIAN_FRONTEND=noninteractive

RUN apt-get update \
    && apt-get install --no-install-recommends -qy coturn python3 python3-pip python3-setuptools curl ca-certificates \
    && pip3 install --no-input j2cli dnspython

# Configuration environment
ENV TURN_REALM= \
    TURN_AUTH_SECRET= \
    TURN_REDIS_USERDB= \
    TURN_TLS_CRT= \
    TURN_TLS_KEY= \
    IP_ADDR_INT= 

# Entrypoint script and jinja templates
COPY turnserver.conf.j2 /root/turnserver.conf.j2
COPY ipcheck.py /usr/local/bin
RUN  chmod +x /usr/local/bin/ipcheck.py

EXPOSE 3478 3478/udp
CMD ["/usr/local/bin/ipcheck.py"]
