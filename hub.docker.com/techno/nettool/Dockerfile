FROM ubuntu:18.04

RUN apt update && apt upgrade -y
RUN apt install -y mysql-client curl wget iputils-ping net-tools dnsutils

CMD ["tail", "-f", "/dev/null"]

