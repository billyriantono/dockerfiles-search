FROM alpine:latest

COPY "cmd.sh" "/root/cmd.sh"

RUN apk update && \
apk add nginx && \
mkdir -p /www/data && \
mkdir -p /run/nginx && \
chmod +x ~/cmd.sh

COPY "default.conf" "/etc/nginx/conf.d"
COPY "index.html" "/www/data"

CMD /root/cmd.sh