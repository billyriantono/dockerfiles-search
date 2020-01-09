FROM ubuntu:bionic
COPY data/texlive.profile /tmp/
COPY data/texlive.sh /etc/profile.d/
WORKDIR /tmp
RUN apt update; apt install -y wget perl perl-modules; \
    mkdir /tmp/install; cd /tmp/install; \
    wget http://mirror.ctan.org/systems/texlive/tlnet/install-tl-unx.tar.gz && \
    tar xvzf install-tl-unx.tar.gz && mv install-tl*/* /tmp; \
    cd /tmp && ./install-tl -repository http://mirror.ctan.org/systems/texlive/tlnet/ \
                            -profile texlive.profile && \
    . /etc/profile.d/texlive.sh; \
    tlmgr install titlesec tabulary varwidth framed wrapfig upquote \
                  capt-of needspace letltxmacro; \
    apt install -y python3 python3-pip; \
    update-alternatives --install /usr/bin/python python /usr/bin/python3 100; \
    update-alternatives --install /usr/bin/pip pip /usr/bin/pip3 100; \
    apt install libffi-dev libssl-dev cmake -y && \
    wget -O- https://github.com/libgit2/libgit2/archive/v0.28.4.tar.gz | tar xz && \
    cd libgit2-0.28.4 && \
    mkdir build && cd build && cmake .. && make -j9 && make install && ldconfig && \
    pip3 install -U pygit2; \
    pip3 install sphinx ; apt clean; \
    dpkg -l | grep -e '-dev' | grep ^ii | awk '{print $2}' | cut -d: -f1 | xargs apt purge --auto-remove -y; \
    cd /; rm -fr /tmp/*
CMD ["/bin/bash", "-l"]
