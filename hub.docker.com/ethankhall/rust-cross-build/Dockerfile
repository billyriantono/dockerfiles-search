FROM archlinux/base

RUN echo $'[archlinuxfr]\n\
SigLevel = Never\n\
Server = http://repo.archlinux.fr/$arch\n' >> /etc/pacman.conf && \
    pacman -Syu --noconfirm && \
    pacman -S --noconfirm yaourt base-devel git wget customizepkg && \
    useradd -m builder && \
    echo "builder ALL=NOPASSWD: ALL" >> /etc/sudoers && \
    mkdir -p /etc/customizepkg.d/ && \
    echo "replace#global#OSX_VERSION_MIN=10.6#OSX_VERSION_MIN=10.7" > /etc/customizepkg.d/osxcross-git
USER builder
WORKDIR /home/builder
RUN yaourt -S --noconfirm osxcross-git mingw-w64-gcc
RUN curl https://sh.rustup.rs -sSf | sh -s -- --default-toolchain nightly -y && \
    echo $'[target.x86_64-apple-darwin]\n\
linker = "x86_64-apple-darwin15-cc"\n\
ar = "x86_64-apple-darwin15-ar"\n\
[target.x86_64-pc-windows-gnu]\n\
linker = "x86_64-w64-mingw32-gcc"\n\
ar = "x86_64-w64-mingw32-gcc-ar"' > ~/.cargo/config && \
    ~/.cargo/bin/rustup target add x86_64-apple-darwin && \
    ~/.cargo/bin/rustup target add x86_64-pc-windows-gnu

ENV PATH=$PATH:/home/builder/.cargo/bin/:/usr/local/osx-ndk-x86/bin:/usr/x86_64-w64-mingw32/bin
