FROM ubuntu:latest

# install openntp
RUN apt-get update && apt-get install -y chrony && apt-get clean && rm -rf /var/lib/apt/lists/*

# use custom ntpd config file
COPY assets/chrony.conf /etc/chrony/chrony.conf

# ntp port
EXPOSE 123/udp

# start ntpd in the foreground
ENTRYPOINT [ "/usr/sbin/chronyd","-d"]
