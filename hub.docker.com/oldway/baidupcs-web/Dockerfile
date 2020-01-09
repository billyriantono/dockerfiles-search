FROM alpine:3.10
LABEL maintainer="oldway <oldway2012@live.com>"
ENV BAIDUPCS_VERSION 3.6.8

WORKDIR /opt

RUN	set -x && \
	apk add --no-cache --update wget unzip && \
	wget --no-check-certificate https://github.com/liuzhuoling2011/baidupcs-web/releases/download/${BAIDUPCS_VERSION}/BaiduPCS-Go-${BAIDUPCS_VERSION}-linux-amd64.zip && \
	unzip BaiduPCS-Go-${BAIDUPCS_VERSION}-linux-amd64.zip && \
	mv BaiduPCS-Go-${BAIDUPCS_VERSION}-linux-amd64 BaiduPCS && \
	rm -rf BaiduPCS-Go-${BAIDUPCS_VERSION}-linux-amd64.zip && \
	apk del wget unzip

VOLUME ["/download"]
VOLUME ["/root/.config/BaiduPCS-Go"]

CMD ["/opt/BaiduPCS/BaiduPCS-Go"]

EXPOSE 5299