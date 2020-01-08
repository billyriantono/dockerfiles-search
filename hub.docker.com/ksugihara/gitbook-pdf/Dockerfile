# Base Image
FROM node:10.11

MAINTAINER KentaSugihara <kenta.sugihara@itage.co.jp>

# インストール準備
RUN apt -qq update && apt -qq -y upgrade

# 日本語の使用設定
ENV LANG ja_JP.UTF-8
ENV LANGUAGE ja_JP:ja

## フォント
RUN apt install -qq -y fonts-ipafont-gothic \
        fonts-ipafont-mincho
    
# GitBook
RUN apt install -qq -y calibre &&\
    npm install -g gitbook-cli &&\
    gitbook fetch latest &&\
    gitbook install