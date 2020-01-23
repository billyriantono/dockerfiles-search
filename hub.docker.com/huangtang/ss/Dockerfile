FROM alpine:3.7

RUN apk add python3 && \
    pip3 install shadowsocks

CMD ssserver -p ${PORT:-443} \
             -k ${PASSWORD:-password} \
             -m ${METHOD:-rc4-md5}
