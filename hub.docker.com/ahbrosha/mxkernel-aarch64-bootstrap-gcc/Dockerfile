# mxkernel/mxkernel-gcc
FROM ahbrosha/mxkernel-aarch64-binutils

ARG BUILD_DIR=/tmp/build

# Add private Key to the docker container
COPY PKGBUILD $BUILD_DIR/PKGBUILD

# Install newlib from git repo
RUN mkdir -p $BUILD_DIR \
    && chown -R nobody:nobody $BUILD_DIR \
    && cd $BUILD_DIR \
    && sudo -u nobody makepkg -s --skippgpcheck \
    && pacman -U --noconfirm aarch64-none-elf-bootstrap-gcc-*.pkg.tar.xz \
    && rm -rf $BUILD_DIR 
