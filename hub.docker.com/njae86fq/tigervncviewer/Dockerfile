FROM alpine:latest AS builder
RUN apk add --no-cache curl
RUN version=1.10.1 \
 && curl -o source.zip -L "https://github.com/TigerVNC/tigervnc/archive/v${version}.zip"
RUN unzip -q source.zip
RUN mv -v /tigervnc-* /tigervnc
WORKDIR /tigervnc
RUN mkdir build
WORKDIR /tigervnc/build
RUN apk add --no-cache cmake make gcc g++ xorg-server-dev libjpeg-turbo-dev libxrandr-dev gettext-dev fltk-dev gnutls-dev linux-pam-dev
# NOTE: As a workaround for build error "undefined reference to `libintl_gettext'",
# skip using dgettext from libc.
# This inserts "set(LIBC_HAS_DGETTEXT false)" line at the very top.
RUN sed -i -e 1iset\(LIBC_HAS_DGETTEXT\ false\) ../CMakeLists.txt
RUN cmake -G "Unix Makefiles" ..
RUN make vncviewer

FROM alpine:latest
RUN apk add --no-cache font-noto libjpeg-turbo libxrandr gettext fltk gnutls linux-pam
COPY --from=builder /tigervnc/build/vncviewer/vncviewer /vncviewer

ENTRYPOINT ["/vncviewer"]
