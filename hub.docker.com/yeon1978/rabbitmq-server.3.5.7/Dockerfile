FROM ubuntu:16.04

# 기본 모듈 설치
RUN apt-get update -y && apt-get upgrade -y && apt-get clean \
    && apt-get install -y software-properties-common vim cron curl wget net-tools telnetd iputils-ping net-tools unzip telnet

# rabbitMQ 설치
RUN apt list --installed rabbitmq-server \
    && apt install -y rabbitmq-server

# 관리용 플러그인 활성화
RUN rabbitmq-plugins enable rabbitmq_management

# Define environment variables.
#ENV RABBITMQ_LOG_BASE /data/log
#ENV RABBITMQ_MNESIA_BASE /data/mnesia

# Define mount points.
#VOLUME ["/data/log", "/data/mnesia"]

# Define working directory
WORKDIR /data

# 서비스 시작
CMD ["rabbitmq-server"]

# Expose ports
EXPOSE 5672
EXPOSE 15672