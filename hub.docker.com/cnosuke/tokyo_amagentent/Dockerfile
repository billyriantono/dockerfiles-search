#
# Mapcrafter Dockerfile
# https://github.com/snugfox/docker-mapcrafter
#

# Pull base build image
FROM alpine:latest as builder

# Define working directory
WORKDIR /usr/src

# Build Mapcrafter
RUN set -x \
    && apk add --no-cache --virtual build-deps \
        boost-dev \
        build-base \
        cmake \
        git \
        libjpeg-turbo-dev \
        libpng-dev \
    && mkdir -p /usr/src \
    && git clone https://github.com/mapcrafter/mapcrafter.git \
    && cmake mapcrafter \
    && make install \
    && apk del --no-cache build-deps

# Pull base image
FROM alpine:latest

# Install dependencies
RUN apk add --no-cache libstdc++ libpng libjpeg-turbo boost-iostreams boost-system boost-filesystem boost-program_options

# Copy built Mapcrafter files
COPY --from=builder /usr/local/share/mapcrafter /usr/local/share/mapcrafter/
COPY --from=builder /usr/local/bin/mapcrafter /usr/local/bin/mapcrafter_markers /usr/local/bin/
COPY --from=builder /usr/local/lib/*.so /usr/local/lib/

# Define entrypoint
ENTRYPOINT [ "/usr/local/bin/mapcrafter" ]
