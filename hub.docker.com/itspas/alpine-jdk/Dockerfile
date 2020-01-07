FROM itspas/alpine:3.3

MAINTAINER yenole <Netxy@vip.qq.com>

# 更新并安装环境
RUN apk add --update openjdk8

# data中的文件
ENV JAR=jar.jar

# 切换到data目录
WORKDIR /data

# 需要挂载data目录
VOLUME /data

# 执行
ENTRYPOINT java -jar $JAR


