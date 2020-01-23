FROM openjdk:alpine
MAINTAINER biboheart "biboheart@qq.com"


ENV PKGNAME=graphicsmagick
ENV PKGVER=1.3.30
ENV PKGSOURCE=http://downloads.sourceforge.net/$PKGNAME/$PKGNAME/$PKGVER/GraphicsMagick-$PKGVER.tar.lz

#
# Installing graphicsmagick dependencies
RUN apk add --no-cache --update g++ \
                     gcc \
                     make \
                     automake \
                     autoconf \
                     git \
                     lzip \
                     wget \
                     sdl-dev \
                     giflib-dev \
                     libjpeg-turbo-dev \
                     lcms2-dev \
                     libwmf-dev \
                     jasper-dev \
                     libx11-dev \
                     libpng-dev \
                     libtool \
                     jasper-dev \
                     bzip2-dev \
                     libxml2-dev \
                     tiff-dev \
                     exiftool \
                     freetype-dev \
                     libgomp
    # GM
RUN wget $PKGSOURCE --no-check-certificate && \
    lzip -d -c GraphicsMagick-$PKGVER.tar.lz | tar -xvf - && \
    cd GraphicsMagick-$PKGVER && \
    ./configure \
      --build=$CBUILD \
      --host=$CHOST \
      --prefix=/usr \
      --sysconfdir=/etc \
      --mandir=/usr/share/man \
      --infodir=/usr/share/info \
      --localstatedir=/var \
      --enable-shared \
      --disable-static \
      --with-modules \
      --with-threads \
      --with-webp=yes \
      --with-bzip=yes \
      --with-tiff=yes \
      --with-freetype=yes \
      --with-jpeg=yes \
      --with-jp2=yes \
      --with-cms2=yes \
      --with-xml=yes \
      --with-x11=yes \
      --with-wmf=yes \
      --with-gs-font-dir=/usr/share/fonts/Type1 \
      --with-quantum-depth=16 && \
    make && \
    make install && \
    cd / && \
    rm -rf GraphicsMagick-$PKGVER && \
    rm GraphicsMagick-$PKGVER.tar.lz && \
    apk del g++ \
            gcc \
            make \
            automake \
            autoconf \
            git \
            lzip \
            wget

CMD [ "/bin/sh" ]
