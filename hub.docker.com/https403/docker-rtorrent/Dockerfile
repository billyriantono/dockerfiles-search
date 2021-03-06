FROM alpine:3.9 as builder

# Install build dependencies
RUN apk add --update \
  build-base \
  git \
  libtool \
  automake \
  autoconf \
  cppunit-dev \
  curl-dev \
  zlib-dev \
  ncurses-dev \
  libressl-dev \
  binutils \
  linux-headers \
  xmlrpc-c-dev

WORKDIR /tmp/

# rTorrent looks for <ncursesw/curses.h>
RUN mkdir -p /usr/include/ncursesw && ln -s /usr/include/curses.h /usr/include/ncursesw/

# Build libtorrent and install into builder stage.
RUN git clone https://github.com/rakshasa/libtorrent.git
RUN cd /tmp/libtorrent && ./autogen.sh && ./configure && make && make install \
  && make install DESTDIR=/tmp/artifacts && cd /tmp/

# Build rTorrent and install into builder stage.
RUN git clone https://github.com/http403/rtorrent.git
RUN cd /tmp/rtorrent && ./autogen.sh && ./configure --with-xmlrpc-c && make \
  && make install DESTDIR=/tmp/artifacts && cd /tmp/

# Runtime stage
FROM alpine:3.9

# Copy the build artifacts from the builder stage.
COPY --from=builder /tmp/artifacts /

# Create privileged user.
# -D disables password
# -g '' specifies empty user information
RUN adduser -D -g '' -h /rtorrent rtorrent

ENTRYPOINT [ "rtorrent" ]

# Install runtime dependencies
RUN apk add --update \
  libstdc++ \
  libgcc \
  libcurl \
  zlib \
  ncurses-libs \
  xmlrpc-c

# Switch to user context.
USER rtorrent
WORKDIR /rtorrent