FROM ubuntu:bionic

RUN \
    apt-get update && \
    apt-get install -qy ssh curl dnsutils tcpdump telnet

CMD ["/bin/bash", "-c", "echo sleeping; trap : TERM INT; sleep infinity & wait"]
