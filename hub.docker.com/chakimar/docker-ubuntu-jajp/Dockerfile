FROM ubuntu

RUN apt-get update && apt-get install -y \
    language-pack-ja-base \
    language-pack-ja \
 && apt-get clean \
 && rm -rf /var/lib/apt/lists/*

ENV LANG ja_JP.UTF-8
ENV TZ Asia/Tokyo