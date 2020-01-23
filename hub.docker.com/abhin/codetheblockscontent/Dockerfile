FROM alpine:3.11.2

RUN apk update                     \
    && apk upgrade                 \
    && apk add --no-cache          \
        bash=5.0.11-r1             \
        build-base=0.5-r1          \
        clang=9.0.0-r1             \
        cmake=3.15.5-r0            \
        g++=9.2.0-r3               \
        gcc=9.2.0-r3               \
        git=2.24.1-r0              \
        git-subtree=2.24.1-r0      \
        linux-headers=4.19.36-r0   \
        make=4.2.1-r2              \
        openssh=8.1_p1-r0          \
        zlib-dev=1.2.11-r3         \
    && rm -rf /var/cache/apk/*
