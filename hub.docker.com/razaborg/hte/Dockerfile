FROM alpine
LABEL maintainer "contact@razaborg.fr"
RUN apk --update add git alpine-sdk lzo-dev libx11 ncurses ncurses-dev automake autoconf bison texinfo flex-dev clang
RUN git clone https://github.com/sebastianbiallas/ht.git
WORKDIR /ht

RUN ./autogen.sh && ./configure --enable-release --enable-static --enable-shared
RUN make; make htdoc.h; make
RUN chmod +x ./install-sh && make install

ENTRYPOINT ["ht"]
