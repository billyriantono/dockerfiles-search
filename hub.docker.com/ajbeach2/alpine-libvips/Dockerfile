FROM alpine:3.9
RUN mkdir /root/scripts
ADD ./compile-libvips.sh /root/scripts/
RUN \
  # Install dependencies
  apk add --update git pkgconf automake pkgconfig curl gcc g++ make libexif-dev libwebp-dev libtool autoconf gobject-introspection-dev \
  libgcc libjpeg-turbo-dev swig gtk-doc libpng-dev gettext giflib-dev glib-dev libxml2-dev

RUN ~/scripts/compile-libvips.sh

FROM alpine:3.9
RUN apk --no-cache add ca-certificates pkgconf linux-headers giflib-dev glib-dev musl-dev gcc libexif-dev libwebp-dev libpng-dev libgcc libjpeg-turbo-dev glib-dev
COPY --from=0 /root/libvips /root/libvips
ENV PKG_CONFIG_PATH $PKG_CONFIG_PATH:/root/libvips/lib/pkgconfig
ENV LD_LIBRARY_PATH=LD_LIBRARY_PATH:/root/libvips/lib
