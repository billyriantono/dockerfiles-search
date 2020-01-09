# mxkernel/mxkernel-binutils
FROM  ahbrosha/mxkernel-base

ARG BUILD_DIR=/tmp/build

# Add private Key to the docker container
COPY PKGBUILD $BUILD_DIR/PKGBUILD

# Install binutils from git repo
RUN chown -R nobody:nobody $BUILD_DIR \
    && cd $BUILD_DIR \
    && sudo -u nobody makepkg -s --skippgpcheck \
    && pacman -U --noconfirm aarch64-none-elf-binutils-*.pkg.tar.xz \
    && rm -rf $BUILD_DIR 
