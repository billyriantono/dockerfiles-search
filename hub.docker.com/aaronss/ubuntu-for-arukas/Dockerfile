FROM debian:latest

MAINTAINER AaronSS

#  Set apt-get to automatically retry if a package download fails
RUN echo 'Acquire::Retries "5";' > /etc/apt/apt.conf.d/99AcquireRetries


RUN apt-get update && apt-get install -y openssh-server git vim python screenfetch && rm -rf /var/lib/apt/lists/* && apt-get clean
RUN echo 'root:root' |chpasswd
RUN sed -ri 's/^PermitRootLogin\s+.*/PermitRootLogin yes/' /etc/ssh/sshd_config
RUN sed -ri 's/UsePAM yes/#UsePAM yes/g' /etc/ssh/sshd_config
EXPOSE 22

ENV SERVER_ADDR 0.0.0.0
ENV SERVER_PORT 2333
ENV PASSWORD    2333
ENV METHOD      aes-256-cfb
ENV PROTOCOL    auth_aes128_md5
ENV OBFS        tls1.2_ticket_auth_compatible
ENV TIMEOUT     300
ENV DNS_ADDR    8.8.8.8
ENV DNS_ADDR_2  8.8.4.4

RUN git clone -b manyuser https://github.com/shadowsocksr/shadowsocksr.git ~/shadowsocksr
#  ENTRYPOINT ["/usr/local/bin/entrypoint.sh"]
CMD python ~/shadowsocksr/shadowsocks/server.py -p $SERVER_PORT -k $PASSWORD -m $METHOD -O $PROTOCOL -o $OBFS
