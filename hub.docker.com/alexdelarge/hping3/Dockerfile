FROM kalilinux/kali-linux-docker:latest
RUN apt-get update -y && \
    apt-get upgrade -y && \
    apt-get install -y hping3 && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/ /tmp/ /var/tmp/*
ENTRYPOINT [ "hping3" ]
