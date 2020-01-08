FROM httpd:2.4

LABEL MAINTAINER="aimergirls"

ENV TZ='Asia/Tokyo'
RUN apt update && \
    apt install -y locales && \
    localedef -i ja_JP -c -f UTF-8 -A /usr/share/locale/locale.alias ja_JP.UTF-8
ENV LANG ja_JP.utf8
