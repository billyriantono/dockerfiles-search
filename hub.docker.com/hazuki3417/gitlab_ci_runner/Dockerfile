# Please execute the following command to build
# docker build -t gitlab_ci_runner this_file_path

# Please execute the following command to start it
# docker run -dit --name gitlab_ci_runner gitlab_ci_runner

# ベースイメージを指定
FROM ubuntu:18.04
# 制作者情報を指定
LABEL maintainer="hazuki3417 <hazuki3417@gmail.com>"

# 環境変数を設定
ENV TZ=Asia/Tokyo
ENV DEBIAN_FRONTEND=noninteractive

# 初期設定（最低限必要なツールをインストール）
RUN apt-get update && \
	apt-get install -y \
		software-properties-common \
		sudo \
		vim \
		tree \
		less \
		curl \
		iproute2

# sudoの設定

# bashの設定
RUN : "bashの設定ファイルを作成する" && { \
	echo 'PS1="\! \$? \u@\h:\W# "'; \
	} >> ~/.bashrc

# aliasの設定
# COPY config/.bash_aliases /root/.bash_aliases

# viの設定
# COPY config/.vimrc /root/.vimrc

# メイン処理

# ミドルウェアのインストール
RUN apt-get update && apt-get install -y \
	software-properties-common \
	&& apt-add-repository -y ppa:ondrej/php

RUN apt-get update && apt-get install -y \
	php7.3

RUN curl -L git.io/nodebrew | perl - setup \
	&& export PATH=$HOME/.nodebrew/current/bin:$PATH \
	&& nodebrew install-binary v12.4.0 \
	&& nodebrew use v12.4.0

# TODO: 日付の設定を追加（引数での設定は使用できない）
 