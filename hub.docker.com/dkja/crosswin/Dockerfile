FROM dkja/gtest

RUN     dpkg --add-architecture i386 \
    &&  apt-get update  \
    && echo "ttf-mscorefonts-installer msttcorefonts/accepted-mscorefonts-eula select true" | debconf-set-selections \
    &&  apt-get install -y g++-mingw-w64 \
                            wine \
                                 \
    &&  rm -rf /var/lib/apt/lists/*