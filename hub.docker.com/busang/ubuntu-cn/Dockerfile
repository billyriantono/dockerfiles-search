FROM ubuntu:19.04

ENV TZ=Asia/Shanghai

RUN sed "s/archive\.ubuntu\.com/mirrors\.aliyun\.com/g" < /etc/apt/sources.list > /etc/apt/sources.list.new \
    && mv /etc/apt/sources.list.new /etc/apt/sources.list \
    && apt update \
    && apt install -y tzdata ca-certificates \
    && ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && \
    echo $TZ > /etc/timezone
