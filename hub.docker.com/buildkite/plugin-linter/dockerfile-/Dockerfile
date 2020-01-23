FROM alpine:latest
ENV LANG=C.UTF-8 TZ=Asia/Shanghai
RUN apk add --no-cache --update tzdata \
&& rm -rf /tmp/* /var/cache/apk/* /var/lib/apk/lists/* 
# && echo 'hosts: files mdns4_minimal [NOTFOUND=return] dns mdns4' > /etc/nsswitch.conf 
CMD ["/bin/sh"]
