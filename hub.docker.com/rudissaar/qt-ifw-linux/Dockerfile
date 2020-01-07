FROM fedora:latest
ADD http://download.qt.io/online/qtsdkrepository/linux_x64/desktop/tools_ifw/qt.tools.ifw.32/3.2.0ifw-linux-x64.7z /tmp/ifw.7z
RUN \
    umask 022 && \
    dnf install -y \
        dbus-libs \
        findutils \
        fontconfig \
        gawk \
        libxcb \
        libxkbcommon-x11 \
        libX11-xcb \
        libXext \
        libXrender \
        p7zip \
        p7zip-plugins \
        upx \
        wget && \
    7z x -aoa /tmp/ifw.7z -o/tmp/ifw && \
    rm /tmp/ifw.7z && \
    cp /tmp/ifw/Tools/QtInstallerFramework/*/bin/* /usr/local/bin/ && \
    rm -r /tmp/ifw && \
    dnf autoremove && \
    dnf clean all
