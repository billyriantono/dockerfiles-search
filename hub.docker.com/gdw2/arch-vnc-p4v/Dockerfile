FROM gdw2/arch-vnc-base

ENV XPROG /root/p4v/bin/p4v

RUN pacman -S --noconfirm --needed tar libxml2
ADD http://filehost.perforce.com/perforce/r14.2/bin.linux26x86_64/p4v.tgz /root/p4v.tgz
RUN tar xzf p4v.tgz
RUN mv p4v-* p4v
