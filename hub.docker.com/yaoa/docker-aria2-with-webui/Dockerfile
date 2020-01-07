FROM alpine:edge

LABEL maintainer "Dean Camera <http://www.fourwalledcubicle.com>"

RUN mkdir -p /conf && \
	mkdir -p /conf-copy && \
	mkdir -p /data && \
	apk add --no-cache tzdata bash aria2 darkhttpd s6

RUN	apk add --no-cache --virtual .install-deps curl unzip \
	&& mkdir -p /aria2-webui \
	&& curl -o /aria2-webui.zip -L https://github.com/ziahamza/webui-aria2/archive/fb9d758d5cdc2be0867ee9502c44fd17560f5d24.zip \
	&& unzip /aria2-webui.zip -d /aria2-webui \
	&& mv /aria2-webui/webui-aria2-fb9d758d5cdc2be0867ee9502c44fd17560f5d24/* /aria2-webui \
	&& rm -rf /aria2-webui/webui-aria2-fb9d758d5cdc2be0867ee9502c44fd17560f5d24 \
	&& rm /aria2-webui.zip \
	&& apk del .install-deps

ADD files/start.sh /conf-copy/start.sh
ADD files/aria2.conf /conf-copy/aria2.conf

RUN chmod +x /conf-copy/start.sh

WORKDIR /

VOLUME ["/data"]
VOLUME ["/conf"]

EXPOSE 6800
EXPOSE 80

CMD ["/conf-copy/start.sh"]
