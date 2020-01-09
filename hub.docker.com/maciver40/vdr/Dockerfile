FROM maciver40/ubuntu-base

LABEL maintainer="robert@eisenmann.email"

VOLUME [ "/config" ]
VOLUME [ "/video" ]

EXPOSE 9981
EXPOSE 9982

RUN \
    apt-get update && \
    apt-get install -y \
        asciidoc \
        libpcre2-dev \
        pkg-config \
        libssl-dev \
        libavahi-client-dev \
        zlib1g-dev \
        libavcodec-dev \
        libavutil-dev \
        libavformat-dev \
        libswscale-dev \
        libxml-parser-perl \
        libterm-readkey-perl \
        libavresample-dev \
        libxml-treepp-perl \
        libipc-system-simple-perl \
        libdatetime-perl \
        libdatetime-format-strptime-perl\
        libdatetime-format-sqlite-perl \
        libdatetime-format-builder-perl \
        libxml-writer-perl \
        libxml-libxml-perl \
        liblingua-preferred-perl \
        libterm-progressbar-perl \
        libunicode-string-perl \
        libdate-manip-perl \
        libfile-slurp-perl \
        libjson-perl \
        gettext \
        cmake \
        libiconv-hook-dev \
        liburiparser-dev \
        libxml-twig-perl \
        debhelper \
        python \
        python-requests \
        libcurl4-gnutls-dev \
        dvb-apps \
        libva-dev \
        libdvbcsa-dev && \
    git clone https://github.com/tvheadend/tvheadend.git /opt/tvheadend && \
    cd /opt/tvheadend && \
    git checkout master && \
    ./configure --enable-libffmpeg_static --enable-hdhomerun_static --enable-dvbcsa && \
    make && make install && \
    # INSTALL XMLTV
    curl -L https://cpanmin.us | perl - App::cpanminus && \
    cpanm --installdeps /patches && \
    git clone https://github.com/XMLTV/xmltv.git /opt/xmltv && \
    cd /opt/xmltv && \
    git checkout master && \
    perl Makefile.PL && \
    make && make install && \ 
    # INSTALL OSCAM
    add-apt-repository ppa:oscam/ppa && \
    apt-get update && \
    apt-get install -y \
        oscam-svn
