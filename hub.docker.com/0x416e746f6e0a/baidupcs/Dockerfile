FROM 0x416e746f6e0a/alpine-base:3.9

# set maintainer label
LABEL MAINTAINER="Anton Chen <contact@antonchen.com>"

RUN \
 echo "**** install build packages ****" && \
 apk add --no-cache --virtual=build-dependencies \
    unzip \
    openssl \
    curl \
    jq && \
 echo "**** install packages ****" && \
 mkdir -p /app/baidupcs-web && \
 BPCSVERSION=$(curl -sX GET "https://api.github.com/repos/liuzhuoling2011/baidupcs-web/releases/latest" \
    | jq -r .tag_name ) && \
 curl -o \
    /tmp/BaiduPCS.zip -L \
    "https://github.com/liuzhuoling2011/baidupcs-web/releases/download/${BPCSVERSION}/BaiduPCS-Go-${BPCSVERSION}-linux-amd64.zip" && \
 unzip /tmp/BaiduPCS.zip -d /tmp && \
 cp -f /tmp/BaiduPCS-Go-${BPCSVERSION}-linux-amd64/BaiduPCS-Go /app/baidupcs-web/ && \
 chmod +x /app/baidupcs-web/BaiduPCS-Go && \
 echo "**** cleanup ****" && \
 apk del --purge \
    build-dependencies && \
 rm -rf \
    /tmp/*


# copy local files
COPY root/ /

# ports and volumes
EXPOSE 5299
VOLUME /downloads
