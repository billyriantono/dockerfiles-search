FROM ubuntu:devel

WORKDIR /root

RUN apt-get update && apt-get install -y --no-install-recommends \
    software-properties-common \
    devscripts \
    gpg-agent \
    fakeroot \
    dput \
 && rm -rf /var/lib/apt/lists/*

RUN sed -ri 's@# (deb-src http://archive.ubuntu.com/ubuntu/ )([^[:space:]-]+)( main restricted)@\1\2\3\n\1\2-updates\3\n\1\2-proposed\3@' /etc/apt/sources.list \
 && apt-get update \
 && apt-get build-dep -y firefox \
 && apt-get source firefox \
 && rm -rf /var/lib/apt/lists/* # redo12

COPY xmonad-fullscreen.patch .

ENV NAME="William Wilhelm" \
    EMAIL="willat8@gmail.com"

RUN cd firefox-* \
 && cp ../xmonad-fullscreen.patch debian/patches \
 && echo "xmonad-fullscreen.patch" >> debian/patches/series \
 && dch -l ppa -D "$(lsb_release -c -s)" "Add xmonad fullscreen fix" \
 && echo "ac_add_options --disable-pulseaudio\nac_add_options --enable-alsa" >> debian/config/mozconfig.in \
 && dch -a "Disable pulseaudio and enable alsa"

ENTRYPOINT ["/bin/bash", "-c", "gpg --import <<<\"$0\" && cd firefox-* && debuild -S && cd .. && LANG=C.UTF-8 dput ppa:willat8/ubuntu-desktop *.changes"]

