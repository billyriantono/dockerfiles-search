FROM mrbluesky125/qtbase

RUN cd /opt/qt5 && make -j$(grep -c ^processor /proc/cpuinfo 2>/dev/null || sysctl -n hw.ncpu) && \
    make install && \
    git submodule foreach --recursive "git clean -dfx" && git clean -dfx

ENV PATH /usr/local/Qt-$QT_VERSION_TAG/bin:$PATH
ENV LD_LIBRARY_PATH /usr/local/Qt-$QT_VERSION_TAG/lib:$LD_LIBRARY_PATH

RUN echo 'export QT_VERSION='QT_VERSION_TAG >> /etc/bash.bashrc
RUN echo 'export PATH='$PATH >> /etc/bash.bashrc
RUN echo 'export LD_LIBRARY_PATH='$LD_LIBRARY_PATH >> /etc/bash.bashrc

WORKDIR /root
