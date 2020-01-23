FROM appimagecrafters/docker-base
ARG FONTCONFIG_VERSION=2.13.92
RUN wget https://www.freedesktop.org/software/fontconfig/release/fontconfig-"$FONTCONFIG_VERSION".tar.gz -O- | tar xz

RUN yum install -y gperf
COPY --from=appimagecrafters/docker-libxml2 /usr/local /usr/local
COPY --from=appimagecrafters/docker-freetype /usr/local /usr/local

RUN source /entrypoint.sh && cd fontconfig-"$FONTCONFIG_VERSION" && ./configure --prefix=/usr/local  --enable-libxml2
RUN source /entrypoint.sh && cd fontconfig-"$FONTCONFIG_VERSION" &&  make all -j$(nproc)
RUN source /entrypoint.sh && cd fontconfig-"$FONTCONFIG_VERSION" && make install
RUN rm -rf fontconfig-"$FONTCONFIG_VERSION"

WORKDIR /tmp