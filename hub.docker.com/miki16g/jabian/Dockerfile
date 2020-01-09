FROM debian:jessie
MAINTAINER Tsuyoshi Morioka <miki16g@gmail.com>

# set locale
RUN apt update
RUN apt install -y locales
RUN locale-gen ja_JP.UTF-8
ENV LANG ja_JP.UTF-8
ENV LC_CTYPE ja_JP.UTF-8
RUN localedef -f UTF-8 -i ja_JP ja_JP.utf8

# set timezone
RUN echo "Asia/Tokyo" > /etc/timezone
RUN rm /etc/localtime
RUN ln -s /usr/share/zoneinfo/Asia/Tokyo /etc/localtime
RUN dpkg-reconfigure -f noninteractive tzdata
