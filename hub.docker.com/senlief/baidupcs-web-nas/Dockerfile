FROM alpine
ENV VERSION 3.6.8
ENV PLATFORM amd64
RUN mkdir /app && wget -O BaiduPCS-Go-$VERSION-linux-$PLATFORM.zip  https://github.com/liuzhuoling2011/baidupcs-web/releases/download/$VERSION/BaiduPCS-Go-$VERSION-linux-$PLATFORM.zip \
    && unzip  BaiduPCS-Go-$VERSION-linux-$PLATFORM.zip && \
    cp BaiduPCS-Go-$VERSION-linux-$PLATFORM/BaiduPCS-Go /app/ && \
    chmod +x /app/BaiduPCS-Go
RUN rm -rf BaiduPCS-Go-$VERSION-linux-$PLATFORM*
VOLUME /root/Downloads
EXPOSE 5299
CMD ["/app/BaiduPCS-Go"]
