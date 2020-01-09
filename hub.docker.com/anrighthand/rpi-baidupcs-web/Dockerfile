FROM resin/raspberrypi3-alpine:edge

LABEL AUTHOR=AnRightHand

ARG ARCH=arm
#ENV BAIDUPCS_WEB_VERSION=$VERSION 
#ENV BAIDUPCS_WEB_URL=https://github.com/liuzhuoling2011/baidupcs-web/releases/download/${BAIDUPCS_WEB_VERSION}/BaiduPCS-Go-${BAIDUPCS_WEB_VERSION}-linux-${ARCH}.zip

WORKDIR /app

RUN  apk add --no-cache wget bash gnupg curl && \
 BAIDUPCS_WEB_VERSION=$(curl -s https://api.github.com/repos/liuzhuoling2011/baidupcs-web/releases/latest --connect-timeout 10| grep 'tag_name' | cut -d\" -f4 ) && \
 BAIDUPCS_WEB_URL=https://github.com/liuzhuoling2011/baidupcs-web/releases/download/${BAIDUPCS_WEB_VERSION}/BaiduPCS-Go-${BAIDUPCS_WEB_VERSION}-linux-${ARCH}.zip && \
 wget $BAIDUPCS_WEB_URL && \
 unzip BaiduPCS-Go-${BAIDUPCS_WEB_VERSION}-linux-${ARCH}.zip && \
 rm BaiduPCS-Go-${BAIDUPCS_WEB_VERSION}-linux-${ARCH}.zip && \
 cd BaiduPCS-Go-${BAIDUPCS_WEB_VERSION}-linux-${ARCH} && \
 mv BaiduPCS-Go .. && cd .. && \
 mv BaiduPCS-Go baidupcs && \
 chmod +x baidupcs

EXPOSE 5299

CMD "/app/baidupcs"
