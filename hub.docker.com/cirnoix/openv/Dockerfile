FROM debian:sid

RUN apt update -y \
        && apt upgrade -y \
        && apt install -y wget unzip qrencode \
        && rm -rf /etc/localtime \
        && ln -sf /usr/share/zoneinfo/Asia/Shanghai /etc/localtime
        
RUN mkdir -m 777 /v2raybin
RUN mkdir -m 777 /caddybin
ADD entrypoint.sh /entrypoint.sh
RUN chmod +x /entrypoint.sh
ENTRYPOINT /entrypoint.sh
EXPOSE 8080