FROM gliderlabs/consul:0.5
ADD ./config /config/
ADD ./check-http /bin/check-http
ADD https://dl.bintray.com/mitchellh/consul/0.5.2_web_ui.zip /tmp/webui.zip
ADD https://get.docker.io/builds/Linux/x86_64/docker-1.6.1 /bin/docker
RUN cd /tmp && unzip webui.zip && mv dist /ui && rm webui.zip && apk add --update curl bash \
	&& rm -rf /var/cache/apk/* && chmod +x /bin/docker /bin/check-http
EXPOSE 8300 8301 8301/udp 8302 8302/udp 8400 8500 53 53/udp
VOLUME ["/data"]
ENTRYPOINT ["/bin/consul", "agent", "-server", "-config-dir=/config"]
