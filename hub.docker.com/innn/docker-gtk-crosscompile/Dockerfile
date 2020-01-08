FROM fedora

COPY install.sh glib.patch /
COPY ssl /usr/x86_64-w64-mingw32/sys-root/mingw/ssl
COPY toolchain-x86_64-w64-mingw32.meson toolchain-x86_64-w64-mingw32-wine.meson /usr/local/share/meson/cross/
RUN chmod +x /install.sh
RUN /install.sh
