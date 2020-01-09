FROM alpine:3.9
LABEL maintainer "Steve Qian"

USER root
ENV BAIDUPCS_VERSION 3.6.7
WORKDIR /

RUN	set -x && \
	apk add --no-cache --update wget unzip && \
	#wget --no-check-certificate http://qiniu.zoranjojo.top/BaiduPCS-Go-${BAIDUPCS_VERSION}-linux-amd64.zip && \
	wget --no-check-certificate https://github.com/liuzhuoling2011/baidupcs-web/releases/download/${BAIDUPCS_VERSION}/BaiduPCS-Go-${BAIDUPCS_VERSION}-linux-amd64.zip && \
	unzip BaiduPCS-Go-${BAIDUPCS_VERSION}-linux-amd64.zip && \
	mv BaiduPCS-Go-${BAIDUPCS_VERSION}-linux-amd64 BaiduPCS && \
	mkdir -p /opt/BaiduPCS && \
	cp -f BaiduPCS/* /opt/BaiduPCS/ && \
	rm -rf BaiduPCS* && \
	apk del wget unzip


CMD ["/opt/BaiduPCS/BaiduPCS-Go"]

EXPOSE 5299
