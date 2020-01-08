FROM resin/armhf-alpine:3.6

MAINTAINER BaseBoxOrg <baseboxorg@outlook.com>

USER root

RUN [ "cross-build-start" ]

RUN addgroup -g 1000 user && \
    adduser -D -u 1000 -G user -s /bin/bash user
    
RUN apk add --no-cache curl ca-certificates python tar \
    && mkdir -p /home/user/.dropbox /home/user/Dropbox /usr/local/bin/dropbox /usr/local/bin/dropbox-cli \
    && curl -Lo dropbox-linux-x86_64.tar.gz https://www.dropbox.com/download?plat=lnx.x86_64 \
    && tar xzfv dropbox-linux-x86_64.tar.gz --strip 1 -C /usr/local/bin/dropbox \
    && rm dropbox-linux-x86_64.tar.gz \
    && curl -Lo dropbox.py https://www.dropbox.com/download?dl=packages/dropbox.py \
    && mv dropbox.py /usr/local/bin/dropbox-cli \
    && chmod +x /usr/local/bin/dropbox-cli \
    && chmod +x /usr/local/bin/dropbox \
    && chown user:user /usr/local/bin/dropbox-cli \
    && chown user:user /usr/local/bin/dropbox \
    && chown user:user -R /home/user/ 

RUN [ "cross-build-end" ]

USER user

WORKDIR /home/user/Dropbox

EXPOSE 17500

VOLUME ["/home/user/Dropbox", "/home/user/.dropbox"]

CMD ["/usr/local/bin/dropbox"]

