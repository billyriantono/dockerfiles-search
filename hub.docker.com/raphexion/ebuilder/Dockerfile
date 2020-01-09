FROM raphexion/builder:latest

RUN \
    apt-get install -y wget

RUN wget -qO- https://developer.arm.com/-/media/Files/downloads/gnu-rm/7-2018q2/gcc-arm-none-eabi-7-2018-q2-update-linux.tar.bz2 | tar xvj --strip-components=1 -C /usr
