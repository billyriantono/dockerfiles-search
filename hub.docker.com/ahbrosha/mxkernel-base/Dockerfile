# mxkernel/mxkernel-base
FROM base/archlinux:2018.08.01

# Main dependencies
RUN pacman -Sy --noconfirm \
    && pacman -S --noconfirm python2 python2-pip gcc make libisoburn grub nasm git wget sudo fakeroot mtools

# Install AspectC++ and PyXB
RUN wget http://aspectc.org:8080/job/Daily/lastSuccessfulBuild/artifact/aspectcpp-linux64-daily.tar.gz \
    && tar -xzf aspectcpp-linux64-daily.tar.gz \
    && mv aspectc++/ac++ /usr/bin/ \
    && mv aspectc++/ag++ /usr/bin/ \
    && rm aspectcpp-linux64-daily.tar.gz \
    && rm -rf aspectc++ \
    && pip2 install PyXB
