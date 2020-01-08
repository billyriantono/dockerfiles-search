FROM debian:buster-slim as build
RUN printf "Package: *\nPin: release a=stable\nPin-Priority: 400\n\nPackage: *\nPin: release a=testing\nPin-Priority: 99\nPin: release a=unstable\nPin-Priority: 99\nPin: release a=experimental\nPin-Priority: 10" > /etc/apt/preferences
RUN echo "deb http://httpredir.debian.org/debian/ testing main contrib non-free" >> /etc/apt/sources.list
RUN echo "deb http://httpredir.debian.org/debian/ unstable main contrib non-free" >> /etc/apt/sources.list
RUN echo "deb http://httpredir.debian.org/debian/ experimental main contrib non-free" >> /etc/apt/sources.list
RUN echo "deb-src http://httpredir.debian.org/debian/ testing main contrib non-free" >> /etc/apt/sources.list
RUN echo "deb-src http://httpredir.debian.org/debian/ unstable main contrib non-free" >> /etc/apt/sources.list
RUN echo "deb-src http://httpredir.debian.org/debian/ experimental main contrib non-free" >> /etc/apt/sources.list
RUN dpkg --add-architecture i386
RUN apt-get update && apt-get --quiet install --yes build-essential devscripts python3 python3-dev python3-pip git screen bc libssl-dev vim libncurses5-dev wget zip flex bison kmod cpio libelf-dev liblz4-tool lz4 rsync
# install gcc-9 and g++-9
RUN apt-get --quiet install --yes -t experimental gcc-9 g++-9 gcc-multilib libstdc++6:i386 libx11-xcb-dev libx11-xcb-dev:i386 libfreetype6-dev libfreetype6-dev:i386 lib32z1-dev
#RUN apt-get build-dep wine
#RUN ln -s /usr/include/freetype2 /usr/include/freetype
# set gcc-9 as default
RUN rm /usr/bin/gcc && ln -s /usr/bin/gcc-9 /usr/bin/gcc
# cleanup
RUN apt-get clean && rm -rf /var/lib/apt/lists/*

From scratch

COPY --from=build / /
LABEL maintainer="Gronkdalonka <gronkdalonka+docker@pferdemitjetpacks.de>"

CMD bash
