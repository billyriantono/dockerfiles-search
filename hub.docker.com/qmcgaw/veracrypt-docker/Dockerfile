ARG BASE_IMAGE=alpine
ARG ALPINE_VERSION=3.9

FROM ${BASE_IMAGE}:${ALPINE_VERSION} AS builder
ARG VERACRYPT_VERSION=1.23
ARG WXWIDGETS_VERSION=3.0.4
RUN apk --update --no-cache --progress -q add build-base yasm pkgconfig fuse-dev
WORKDIR /wxwidgets
RUN wget -q https://github.com/wxWidgets/wxWidgets/releases/download/v${WXWIDGETS_VERSION}/wxWidgets-${WXWIDGETS_VERSION}.tar.bz2 && \
    tar -xf wxWidgets-${WXWIDGETS_VERSION}.tar.bz2 --strip-components=1 && \
    rm wxWidgets-${WXWIDGETS_VERSION}.tar.bz2
WORKDIR /veracrypt
RUN wget -q https://github.com/veracrypt/VeraCrypt/archive/VeraCrypt_${VERACRYPT_VERSION}.tar.gz && \
    tar -xf VeraCrypt_${VERACRYPT_VERSION}.tar.gz --strip-components=1 && \
    rm VeraCrypt_${VERACRYPT_VERSION}.tar.gz
WORKDIR /veracrypt/src
# To fix for scratch Docker image...
# RUN sed -i '/^export CFLAGS := -Wall/ s/$/ -static/' Makefile && \
#     sed -i '/^export CXXFLAGS := -Wall -Wno-unused-parameter/ s/$/ -static/' Makefile && \
#     sed -i '/^C_CXX_FLAGS := -MMD -D_FILE_OFFSET_BITS=64 -D_LARGEFILE_SOURCE -D_LARGE_FILES -I$(BASE_DIR) -I$(BASE_DIR)\/Crypto/ s/$/ -static/' Makefile
RUN make NOGUI=1 WXSTATIC=1 WX_ROOT=/wxwidgets wxbuild
RUN make NOGUI=1 WXSTATIC=1
RUN ldd Main/veracrypt

FROM ${BASE_IMAGE}:${ALPINE_VERSION}
ARG BUILD_DATE
ARG VCS_REF
LABEL org.label-schema.schema-version="1.0.0-rc1" \
    maintainer="quentin.mcgaw@gmail.com" \
    org.label-schema.build-date=$BUILD_DATE \
    org.label-schema.vcs-ref=$VCS_REF \
    org.label-schema.vcs-url="https://github.com/qdm12/veracrypt-docker" \
    org.label-schema.url="https://github.com/qdm12/veracrypt-docker" \
    org.label-schema.vcs-description="Contains the Veracrypt binary program" \
    org.label-schema.vcs-usage="https://github.com/qdm12/veracrypt-docker/blob/master/README.md#setup" \
    org.label-schema.docker.cmd="docker run -it --rm qmcgaw/veracrypt-docker" \
    org.label-schema.docker.cmd.devel="docker run -it --rm qmcgaw/veracrypt-docker" \
    org.label-schema.docker.params="" \
    org.label-schema.version="1.23" \
    image-size="13.8MB" \
    ram-usage="MB" \
    cpu-usage=""
COPY --from=builder /veracrypt/src/Main/veracrypt /veracrypt
RUN apk add --update --no-cache --progress -q fuse libstdc++ libgcc device-mapper
ENTRYPOINT [ "/veracrypt" ]
CMD [ "--help" ]
