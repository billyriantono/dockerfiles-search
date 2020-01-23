FROM bitnami/minideb:latest

RUN apt-get update -y && apt-get install python3 python3-pip libjemalloc-dev git procps -y

ENV PYTHONDONTWRITEBYTECODE 1
ENV PYTHONUNBUFFERED 1

RUN echo 'alias jemalloc="LD_PRELOAD=/usr/lib/x86_64-linux-gnu/libjemalloc.so"' >> ~/.bashrc
