FROM golang
MAINTAINER dingdayu <614422099@qq.com>

# 更新软件包
RUN apt-get update && apt-get install -y xz-utils \
    && rm -rf /var/lib/apt/lists/*

# 下载 upx
ADD https://github.com/upx/upx/releases/download/v3.95/upx-3.95-amd64_linux.tar.xz /usr/local

# 解压 upx
RUN xz -d -c /usr/local/upx-3.95-amd64_linux.tar.xz | tar -xOf - upx-3.95-amd64_linux/upx > /bin/upx && \
    chmod a+x /bin/upx