FROM golang:alpine as builder

MAINTAINER Takumi Takahashi <takumiiinn@gmail.com>

ARG ZLIB_URL=https://github.com/madler/zlib.git
ARG ZLIB_VER=v1.2.11
ARG LIBGIT2_URL=https://github.com/libgit2/libgit2.git
ARG LIBGIT2_VER=v0.28.2

ARG GIT2GO_URL=https://github.com/libgit2/git2go.git

RUN echo Start! \
 && set -ex \
 && apk add --no-cache build-base gcc wget git python ca-certificates libtool pkgconfig automake autoconf ninja linux-headers cmake openssl-dev curl-dev libssh2-dev zlib-dev \
 && NPROC=$(grep -c ^processor /proc/cpuinfo 2>/dev/null || 1) \
 && mkdir -pv /src /bld \
 && git clone --depth 1 -b $ZLIB_VER $ZLIB_URL /src/zlib \
 && ln -s /src/zlib /bld/zlib && cd /bld/zlib \
 && ./configure \
 && make -j $NPROC \
 && make -j $NPROC install \
 && ldconfig /usr/local/lib \
 && git clone --depth 1 -b $LIBGIT2_VER $LIBGIT2_URL /src/libgit2 \
 && mkdir -p /bld/libgit2-shared && cd /bld/libgit2-shared \
 && cmake -G Ninja -D CMAKE_LIBRARY_PATH=/usr/local/lib -D CMAKE_C_FLAGS=-fPIC -D CMAKE_BUILD_TYPE=RelWithDebInfo -D BUILD_SHARED_LIBS=ON /src/libgit2 \
 && cmake --build . \
 && cmake --build . --target install \
 && ldconfig /usr/local/lib \
 && mkdir -p /bld/libgit2-static && cd /bld/libgit2-static \
 && cmake -G Ninja -D CMAKE_LIBRARY_PATH=/usr/local/lib -D CMAKE_C_FLAGS=-fPIC -D CMAKE_BUILD_TYPE=RelWithDebInfo -D BUILD_SHARED_LIBS=OFF /src/libgit2 \
 && cmake --build . \
 && cmake --build . --target install \
 && ldconfig /usr/local/lib \
 && cd / \
 && export GOPATH="/go" \
 && export PATH="$GOPATH/bin:/usr/local/go/bin:$PATH" \
 && mkdir -p "$GOPATH/src" "$GOPATH/bin" \
 && mkdir -p "$GOPATH/src/github.com/libgit2" \
 && git clone --depth 1 $GIT2GO_URL "$GOPATH/src/github.com/libgit2/git2go" \
 && sed -i -e 's@ -I${SRCDIR}/static-build/install/include@ -I/usr/include@' $GOPATH/src/github.com/libgit2/git2go/git_static.go \
 && sed -i -e 's@ -L${SRCDIR}/static-build/install/lib/@ -L/usr/lib@' $GOPATH/src/github.com/libgit2/git2go/git_static.go \
 && sed -i -e 's@pkg-config: --static ${SRCDIR}/static-build/install/lib/pkgconfig/libgit2.pc@LDFLAGS: -static -L/usr/lib -lgit2 -lcrypto -lcurl -lssh2 -lssl -lz /usr/local/lib/libz.a /usr/lib/libcurl.a /usr/local/lib/libgit2.a /usr/lib/libssh2.a /usr/lib/libssl.a /usr/lib/libcrypto.a@' $GOPATH/src/github.com/libgit2/git2go/git_static.go \
 && cd "$GOPATH/src/github.com/libgit2/git2go" \
 && go install -tags "static" -ldflags "-extldflags '-static'" ./... \
 && go run -tags "static" -ldflags "-extldflags '-static'" script/check-MakeGitError-thread-lock.go \
 && go version \
 && rm -rf /src /bld \
 && echo Complete!

ENV GOPATH /go
ENV PATH $GOPATH/bin:/usr/local/go/bin:$PATH

WORKDIR $GOPATH
