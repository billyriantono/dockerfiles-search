FROM amazonlinux

# 作成したユーザの情報
MAINTAINER m2-namiki <m-namiki@bns-g.com>

ENV PACKAGES="wget git vim"

# yumのアップデートとパッケージのインストール
RUN yum -y update && yum install -y ${PACKAGES}
