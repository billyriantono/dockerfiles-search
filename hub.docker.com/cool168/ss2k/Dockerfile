FROM ubuntu:16.04


# Switches deb source to China mirror
#RUN sed -i.bak 's/archive/cn\.archive/' /etc/apt/sources.list

RUN apt-get update && apt-get install -y --no-install-recommends apg
	

# Deploys files

RUN mkdir -p /app
RUN mkdir -p /app/kcp
RUN chmod +x /app
COPY ./client_linux_amd64 /app/kcp
COPY ./server_linux_amd64 /app/kcp
RUN chmod +x /app/kcp/client_linux_amd64
RUN chmod +x /app/kcp/server_linux_amd64

COPY ./packages/*.deb /app/
COPY ./*.sh /app/
RUN chmod +x /app/*.sh

RUN	dpkg -i /app/libmbedcrypto0_*.deb
RUN	dpkg -i /app/shadowsocks-libev_*.deb
RUN	rm /etc/init.d/shadowsocks-libev

RUN     rm -rf /app/*.deb
RUN apt-get clean
RUN rm -rf /var/lib/apt/lists/*
WORKDIR /app
