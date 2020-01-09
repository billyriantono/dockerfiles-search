FROM ubuntu:18.04
ENV LANG=C.UTF-8 TZ=Asia/Shanghai
COPY etc/localtime etc/timezone /etc/
RUN apt-get update && apt-get install tzdata -y  && rm -rf /var/lib/apt/lists/*
CMD ["/bin/sh"]
