FROM graychen/alpine-php7.1:alpine

RUN docker-php-ext-install exif && \ 
docker-php-ext-configure exif && \
apk add --update nodejs npm && \
apk add --no-cache --virtual dumb-init curl make gcc g++ python linux-headers binutils-gold gnupg libstdc++ nss nodejs nodejs-npm \
  alsa-lib \
  at-spi2-atk \
  atk \
  cairo \
  cups-libs \
  dbus-libs \
  eudev-libs \
  expat \
  flac \
  gdk-pixbuf \
  glib \
  libgcc \
  libjpeg-turbo \
  libpng \
  libwebp \
  libx11 \
  libxcomposite \
  libxdamage \
  libxext \
  libxfixes \
  tzdata \
  libexif \
  udev \
  xvfb \
  zlib-dev \
  chromium \
  chromium-chromedriver && \
npm install puppeteer-core && \
apk del --no-cache make gcc g++ python binutils-gold gnupg libstdc++ && \
docker-php-ext-install sockets
