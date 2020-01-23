FROM ubuntu:18.04

RUN apt update && \
    apt --yes install wget xz-utils cmake gcc build-essential libfontconfig1-dev pkg-config libjpeg-dev gnome-common libglib2.0-dev gtk-doc-tools libyelp-dev yelp-tools gobject-introspection libsecret-1-dev libnautilus-extension-dev libopenjp2-7 libopenjp2-7-dev && \
    wget https://poppler.freedesktop.org/poppler-0.65.0.tar.xz && \    
    unxz poppler-0.65.0.tar.xz && \
    tar xf poppler-0.65.0.tar && \
    cd poppler-0.65.0 && \
    cmake  -DCMAKE_BUILD_TYPE=Release   \
           -DCMAKE_INSTALL_PREFIX=/usr  \
           -DENABLE_XPDF_HEADERS=ON && \
    make install       





