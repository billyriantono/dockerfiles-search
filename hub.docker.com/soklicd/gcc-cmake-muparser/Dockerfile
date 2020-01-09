FROM rikorose/gcc-cmake:gcc-6

RUN cd /tmp \
    && wget https://github.com/beltoforion/muparser/archive/v2.2.6.1.tar.gz \
    && tar -xzf v2.2.6.1.tar.gz \
    && cd muparser-2.2.6.1 \
    && ./configure \
    && make -j2 \
    && make install \
    && cd /tmp \
    && rm v2.2.6.1.tar.gz \
    && rm -rf muparser-2.2.6.1
