# 引用说明：https://github.com/HP41/NSISDocker
FROM debian:experimental

ENV TZ="Asia/Shanghai" \
  DEBIAN_FRONTEND=noninteractive

RUN apt-get clean
RUN apt-get update \
  && apt-get install -y \
  ca-certificates \
  bash \
  tar \
  git \
  openssl \
  curl \
  wget \
  unzip \
  locales \
  tzdata

RUN echo "Asia/Shanghai" > /etc/timezone \
  && ln -sf /usr/share/zoneinfo/Asia/Shanghai /etc/localtime \
  && rm -rf /var/lib/apt/lists/* \
  && localedef -i en_US -c -f UTF-8 -A /usr/share/locale/locale.alias en_US.UTF-8 \
  && dpkg-reconfigure -f noninteractive tzdata

RUN apt-get -t experimental update \
  && apt-get install -y mingw-w64 wine \
  && apt-get install -t experimental -y nsis=3.04-2 nsis-pluginapi \
  && apt-get clean

ENV ELECTRON_VER="v7.1.3"
RUN curl -fsSL "https://github.com/electron/electron/releases/download/$ELECTRON_VER/electron-$ELECTRON_VER-win32-ia32.zip" --output /win.zip \
  && mkdir -p /electron/win \
  && unzip /win.zip -d /electron/win \
  && rm -rf /win.zip \
  && rm -rf /electron/win/resources/*.asar \
  && curl -fsSL "https://github.com/electron/electron/releases/download/$ELECTRON_VER/electron-$ELECTRON_VER-darwin-x64.zip" --output /osx.zip \
  && mkdir -p /electron/osx \
  && unzip /osx.zip -d /electron/osx \
  && rm -rf /osx.zip \
  && rm -rf /electron/osx/Electron.app/Contents/Resources/*.asar \
  && rm -rf /electron/osx/Electron.app/Contents/Resources/*.icns

# ENTRYPOINT ["makensis", "-V4"]
# docker run -it \
#   -v /path/to/project/on/host:/path/to/project/on/container \
#   hp41/nsis:3.01-1 \
#   /path/to/project/on/container/installer.nsi
