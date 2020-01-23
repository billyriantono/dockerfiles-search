FROM ubuntu
ENV DEBIAN_FRONTEND noninteractive

RUN apt-get update && apt-get upgrade -y && apt-get install -y --no-install-recommends dnsmasq && rm --recursive --force /var/lib/apt/lists/*

EXPOSE 53/tcp 67/tcp 68/tcp 69/tcp 53/udp 67/udp 68/udp 69/udp
ENTRYPOINT ["dnsmasq", "-k"]


# docker build . -t 192.168.105.200:5000/dnsmasq
# docker push 192.168.105.200:5000/dnsmasq

