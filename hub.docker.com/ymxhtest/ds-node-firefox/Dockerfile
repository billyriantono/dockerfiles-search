# !!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!
# NOTE: DO *NOT* EDIT THIS FILE.  IT IS GENERATED.
# PLEASE UPDATE Dockerfile.txt INSTEAD OF THIS FILE
# !!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!
FROM ymxhtest/ds-node-base:3.9.1
MAINTAINER ymxhtest <ymxhtest@163.com>

USER root

#=========
# Firefox
#=========
ARG FIREFOX_VERSION=45.0
RUN apt-get update -qqy \
  && apt-get -qqy --no-install-recommends install firefox \
  && rm -rf /var/lib/apt/lists/* /var/cache/apt/* \
  && wget --no-verbose -O /tmp/firefox.tar.bz2 http://ftp.mozilla.org/pub/firefox/releases/$FIREFOX_VERSION/linux-x86_64/zh-CN/firefox-$FIREFOX_VERSION.tar.bz2 \
  && apt-get -y purge firefox \
  && rm -rf /opt/firefox \
  && tar -C /opt -xjf /tmp/firefox.tar.bz2 \
  && rm /tmp/firefox.tar.bz2 \
  && mv /opt/firefox /opt/firefox-$FIREFOX_VERSION \
  && ln -fs /opt/firefox-$FIREFOX_VERSION/firefox /usr/bin/firefox

#====================
# 解决ubuntu中启动firefox报错
# XPCOMGlueLoad error for file /opt/firefox-45.0/libxul.so:
# libasound.so.2: cannot open shared object file: No such file or directory
# Couldn't load XPCOM.
#====================
RUN apt-get update -qqy \
  && apt-get -qqy install libasound2 \
  && apt-get -qqy install libgtk2.0-0

#============================================================
# GeckoDriver,由于是selenium2，所以支持47版本以下的浏览器,不需要geckodriver，则先注释
# 当使用Selenium3,其他浏览器版本时，去掉注释即可
#============================================================
ARG GECKODRIVER_VERSION=0.15.0
RUN wget --no-verbose -O /tmp/geckodriver.tar.gz https://github.com/mozilla/geckodriver/releases/download/v$GECKODRIVER_VERSION/geckodriver-v$GECKODRIVER_VERSION-linux64.tar.gz \
  && rm -rf /opt/geckodriver \
  && tar -C /opt -zxf /tmp/geckodriver.tar.gz \
  && rm /tmp/geckodriver.tar.gz \
  && mv /opt/geckodriver /opt/geckodriver-$GECKODRIVER_VERSION \
  && chmod 755 /opt/geckodriver-$GECKODRIVER_VERSION \
  && ln -fs /opt/geckodriver-$GECKODRIVER_VERSION /usr/bin/geckodriver

COPY generate_config /opt/selenium/generate_config
RUN chmod +x /opt/selenium/generate_config \
  && chown -R seluser:seluser /opt/selenium

USER seluser
