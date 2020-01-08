ARG ubuntu_version=18.04
FROM ubuntu:${ubuntu_version} as build
ARG uname_r=4.15.0-36-generic

RUN grep -q '^deb-src' /etc/apt/sources.list || \
  sed -e 's/^deb /deb-src /g' /etc/apt/sources.list >/etc/apt/sources.list.d/deb-src.list

RUN apt-get update && \
  apt-get install -y build-essential bison flex

# Enable more perf features by compiling with various dev packages present
RUN apt-get install -y \
  binutils-dev \
  libaudit-dev \
  libbz2-dev \
  libdw-dev \
  libelf-dev \
  libiberty-dev \
  liblzma-dev \
  libslang2-dev \
  libssl-dev \
  libunwind-dev \
  systemtap-sdt-dev \
  zlib1g-dev

WORKDIR /src
RUN apt-get source "linux-tools-${uname_r}"

RUN ln -s linux-* linux

WORKDIR /src/linux/tools/perf

COPY patches/ /src/patches/
RUN for patch in /src/patches/*.patch; do patch -p3 <"${patch}"; done

# Compile perf statically
RUN make LDFLAGS=-static NO_GTK2=1 NO_LIBNUMA=1 NO_LIBPERL=1 NO_LIBPYTHON=1 NO_JVMTI=1 

FROM scratch

COPY --from=build /src/linux/tools/perf/perf /
COPY --from=build /src/linux/tools/perf/perf-archive.sh /perf-archive
