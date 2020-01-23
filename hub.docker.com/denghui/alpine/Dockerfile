FROM alpine:3.7
MAINTAINER denghui <denghui0115@163.com>

# update apk add mirrors
# RUN echo -e "https://mirrors.aliyun.com/alpine/v3.7/main\n\
# https://mirrors.aliyun.com/alpine/v3.7/community" > /etc/apk/repositories && \
RUN apk update && apk add --no-cache ca-certificates tzdata && \
ln -sf /usr/share/zoneinfo/Asia/Shanghai /etc/localtime && \
echo "Asia/Shanghai" > /etc/timezone
    
