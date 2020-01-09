# mxkernel/mxkernel-newlib
FROM ahbrosha/mxkernel-aarch64-bootstrap-gcc

ARG BUILD_DIR=/tmp/build

# Add private Key to the docker container
COPY PKGBUILD $BUILD_DIR/PKGBUILD

# Install newlib from git repo
RUN mkdir -p $BUILD_DIR \
    && chown -R nobody:nobody $BUILD_DIR \
    && cd $BUILD_DIR \
    && sudo -u nobody makepkg -s --skippgpcheck \
    && pacman -U --noconfirm aarch64-none-elf-newlib-*.pkg.tar.xz \
    && rm -rf $BUILD_DIR 
