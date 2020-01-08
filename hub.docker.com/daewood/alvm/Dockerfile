FROM daewood/asshd

MAINTAINER daewood <daewood@qq.com>

RUN apk --update add nodejs git imagemagick \
    && rm -rf /var/cache/apk/* /src

COPY rootfs/ /
	
VOLUME [ "/app"]
WORKDIR /app
EXPOSE 3000
ENTRYPOINT ["/init"]

