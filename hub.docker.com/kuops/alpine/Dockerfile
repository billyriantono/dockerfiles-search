FROM alpine:3.10

LABEL maintainer="opshsy@gmail.com"

ENV TZ=Asia/Shanghai
ENV PS1="[\u@\h \W]\$ "

RUN sed -i 's/dl-cdn.alpinelinux.org/mirrors.aliyun.com/g' /etc/apk/repositories \
    && apk add --no-cache tzdata \
          bash \
          curl \
          iproute2 \
          busybox-extras \
    && rm -rf /var/cache/apk/*

CMD [ "/bin/bash" ]
