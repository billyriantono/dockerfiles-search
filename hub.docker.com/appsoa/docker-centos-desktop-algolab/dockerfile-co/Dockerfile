FROM appimagecrafters/docker-base
ARG LIBXML2_VERSION=2.9.9
ARG BUILD_DIR=/tmp/libxml2
RUN git clone https://gitlab.gnome.org/GNOME/libxml2.git --recursive --depth=1 -b v"$LIBXML2_VERSION" ${BUILD_DIR}

COPY --from=appimagecrafters/docker-autoconf /usr/local /usr/local
RUN yum install -y libtool python-devel

RUN source /entrypoint.sh && cd ${BUILD_DIR} && ./autogen.sh --prefix=/usr/local
RUN source /entrypoint.sh && cd ${BUILD_DIR} && make all -j`nproc`
RUN source /entrypoint.sh && cd ${BUILD_DIR} && make install
RUN rm -rf ${BUILD_DIR}

WORKDIR /tmp