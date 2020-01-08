FROM ubuntu:16.04
MAINTAINER fghpdf <quxiangxuan@shimo.im>

ADD https://shimo-static.oss-cn-beijing.aliyuncs.com/google-chrome-unstable_current_amd64.deb /src/chrome-headless.deb

RUN sed -i 's/archive.ubuntu.com/mirrors.163.com/g' /etc/apt/sources.list
RUN apt-get update && apt-get install -y \
  software-properties-common \
  ca-certificates \
  gconf-service \
  fonts-liberation \
  libappindicator1 \
  wget \
  libasound2 \
  libatk1.0-0 \
  libcairo2 \
  libcups2 \
  libgdk-pixbuf2.0-0 \
  libgtk-3-0 \
  libpango-1.0-0 \
  libpangocairo-1.0-0 \
  libx11-xcb1 \
  libgconf-2-4 \
  libglib2.0-0 \
  libnspr4 \
  libnss3 \
  libxss1 \
  libxtst6 \
  libxrender1 \
  libfreetype6 \
  libfontconfig1 \
  libxrandr2 \
  libc6 \
  zlib1g \
  xdg-utils \
  --no-install-recommends && \
  dpkg -i '/src/chrome-headless.deb' && \
  rm -rf /var/lib/apt/lists/*

EXPOSE 9222
