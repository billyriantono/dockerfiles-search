FROM alpine:3.9

LABEL MAINTAINER="yoojiachen@gmail.com"

COPY frpc /usr/local/bin

ONBUILD COPY client.ini /etc/frp/

CMD [ "frpc", "-c", "/etc/frp/client.ini" ]`