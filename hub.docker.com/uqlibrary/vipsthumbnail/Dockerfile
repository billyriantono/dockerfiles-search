FROM uqlibrary/alpine:3.10.2

WORKDIR /usr/local/src

ARG OPENSLIDE_VERSION=3.4.1
ARG OPENSLIDE_URL=https://github.com/openslide/openslide/releases/download
ARG VIPS_VERSION=8.8.3
ARG VIPS_URL=https://github.com/libvips/libvips/releases/download
ENV BUILD_DEPS build-base autoconf automake libtool bc
ENV LIBVIPS_DEPS zlib-dev libxml2-dev jpeg-dev openjpeg-dev tiff-dev \
               glib-dev gdk-pixbuf-dev sqlite-dev libjpeg-turbo-dev libexif-dev lcms2-dev fftw-dev giflib-dev \
               libpng-dev libwebp-dev orc-dev poppler-dev librsvg-dev libgsf-dev openexr-dev gtk-doc \
               msttcorefonts-installer fontconfig

COPY openslide-init.patch /usr/local/src
COPY ./bootstrap.sh /opt/bootstrap.sh
COPY ./timeout.sh /opt/timeout.sh

RUN apk --update --no-cache add ${BUILD_DEPS} ${LIBVIPS_DEPS} \
    # ms fonts
    && update-ms-fonts \
        && fc-cache -f \
	# openslide
	&& wget ${OPENSLIDE_URL}/v${OPENSLIDE_VERSION}/openslide-${OPENSLIDE_VERSION}.tar.gz \
        && tar xf openslide-${OPENSLIDE_VERSION}.tar.gz \
        && patch -p0 <openslide-init.patch \
        && cd openslide-${OPENSLIDE_VERSION} \
        && ./configure --enable-static LDFLAGS=-static \
        && make \
        && make install \
    # vips
    && wget ${VIPS_URL}/v${VIPS_VERSION}/vips-${VIPS_VERSION}.tar.gz \
        && tar xf vips-${VIPS_VERSION}.tar.gz \
        && cd vips-${VIPS_VERSION} \
        && ./configure --enable-static LDFLAGS=-static \
        && make V=0 \
        && make install \
    # clean up
    && rm -rf /usr/local/src/* /usr/local/man/* /usr/local/share/man/* \
    && apk del ${BUILD_DEPS} > /dev/null 2>&1 ||: \
    # boostrap
    && chmod +x /opt/bootstrap.sh \
    && chmod +x /opt/timeout.sh \
    && mkdir -p /tmp/libvips

ENTRYPOINT ["/opt/timeout.sh"]​
