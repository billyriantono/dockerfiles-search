#### Build Container ####
FROM alpine as builder

# Add deps
RUN apk --no-cache add \
         autoconf \
         build-base \
         git \
         libsodium-dev

# Clone source from GitHub
RUN git clone --depth 1 https://github.com/cathugger/mkp224o.git /usr/src/mkp224o

# Build
WORKDIR /usr/src/mkp224o
RUN ./autogen.sh
# x86_64 optimised configure options taken from OPTIMISATION.txt file in Git repo
RUN ./configure --enable-amd64-51-30k --enable-intfilter
RUN make


#### Runtime Container ####
FROM alpine
LABEL maintainer "Alex Haydock <alex@alexhaydock.co.uk>"

COPY --from=builder /usr/src/mkp224o/mkp224o /usr/bin/mkp224o

RUN apk --no-cache add libsodium

WORKDIR /tmp
ENTRYPOINT ["/usr/bin/mkp224o"]
