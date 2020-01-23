FROM multiarch/alpine:armhf-latest-stable

ARG FB_VERSION=v2.0.12

RUN apk --no-cache add ca-certificates

RUN wget https://github.com/filebrowser/filebrowser/releases/download/$FB_VERSION/linux-armv7-filebrowser.tar.gz \
	&& tar xzvf linux-armv7-filebrowser.tar.gz \
	&& rm linux-armv7-filebrowser.tar.gz

ENTRYPOINT [ "/filebrowser" ]