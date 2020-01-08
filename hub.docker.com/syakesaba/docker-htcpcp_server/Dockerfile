FROM ubuntu:latest
MAINTAINER SYA-KE
#docker build -t htcpcp_server .
#docker run -ti -p 8080:8080 htcpcp_server #Ctrl+pq

RUN apt-get -y update && apt-get install -y gcc unzip scapy telnet
ADD https://github.com/madmaze/HTCPCP/archive/master.zip /root/master.zip
WORKDIR /root/
RUN unzip master.zip
WORKDIR /root/HTCPCP-master
RUN sh ./make.em
EXPOSE 8080
ADD ./entrypoint.sh /entrypoint.sh
ADD ./htcpcp.cap /htcpcp.cap
RUN chmod +x /entrypoint.sh
ENTRYPOINT ["/entrypoint.sh"]
