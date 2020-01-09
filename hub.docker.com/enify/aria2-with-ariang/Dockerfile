FROM alpine:latest

MAINTAINER enify <mikucube@outlook.com>


RUN apk update && \
    apk add aria2 && \
    apk add darkhttpd && \
    apk add wget && \
        mkdir /webgui && \
        DOWNLOAD_URL=$(wget -q -O - "https://api.github.com/repos/mayswind/AriaNg/releases/latest" | awk '/browser_download_url/{print $4;exit}' FS='[""]') && \
        wget -qO webgui.zip $DOWNLOAD_URL && \
        unzip webgui.zip -d /webgui && \
        rm webgui.zip && \
        apk del wget && \
    mkdir /download

COPY conf /conf

EXPOSE 6800
EXPOSE 80

ENTRYPOINT ["/conf/startup.sh"]
