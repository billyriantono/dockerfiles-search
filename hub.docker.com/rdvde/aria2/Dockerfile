FROM rdvde/aria2:linux as builder
FROM alpine:latest

ARG  AriaNg_VER=1.1.1

ENV RPC_SECRET=
ENV SECRETAUTO=YES
ENV TRACKERSAUTO=YES
ENV TZ=Asia/Shanghai

COPY  root /
COPY entrypoint.sh /entrypoint.sh
COPY --from=builder  /usr/bin/aria2c  /usr/local/bin/aria2c


RUN apk add --no-cache bash ca-certificates darkhttpd tzdata \
&& rm -rf /var/cache/apk/*  \
&& wget https://github.com/mayswind/AriaNg/releases/download/${AriaNg_VER}/AriaNg-${AriaNg_VER}.zip  \
&& mkdir -p /usr/local/aria2/AriaNg/js/Originaljs \ 
&& unzip -d /usr/local/aria2/AriaNg    AriaNg-${AriaNg_VER}.zip  \
&& rm  AriaNg-${AriaNg_VER}.zip \   
&& cp /usr/local/aria2/AriaNg/js/aria-ng* /usr/local/aria2/AriaNg/js/Originaljs \ 
&& chmod a+x /usr/local/bin/aria2c   \  
&& chmod a+x /usr/local/aria2/updatetrackers.sh \
&& chmod +x /entrypoint.sh \
&& addgroup -g 1000 -S alpine \
&& adduser -u 1000 -G alpine -h /home/alpine -D alpine \
&& mkdir -p /Downloads \
&& chown -R alpine /Downloads/ \
&& mkdir -p /config \
&& cp /usr/local/aria2/defaults/aria2.conf  /config/aria2.conf \
&& touch /config/aria2.session \
&& touch /config/dht.dat \
&& chown -R alpine /config/ \
&& chown -R alpine /usr/local/aria2

USER alpine

EXPOSE 6800  8080  6881  6881/udp
CMD /entrypoint.sh
