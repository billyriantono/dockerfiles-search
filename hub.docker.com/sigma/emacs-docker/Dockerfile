from alpine:3.7

arg EMACS_REPOSITORY="git://git.sv.gnu.org/emacs.git"
arg EMACS_BRANCH="emacs-26"

env CANNOT_DUMP=yes

run apk add --no-cache git curl python libxml2 gnutls

run apk add --no-cache --virtual .build-deps \
        make gcc git autoconf automake linux-headers paxmark gawk \
        glib-dev libxml2-dev gnutls-dev musl-dev ncurses-dev && \
    git clone --depth 1 --branch $EMACS_BRANCH $EMACS_REPOSITORY /tmp/emacs && \
    cd /tmp/emacs && \
    ./autogen.sh && \
    ./configure --without-makeinfo && \
    make install && \
    rm -rf /tmp/emacs && \
    apk del .build-deps

run curl -fsSL https://raw.githubusercontent.com/cask/cask/master/go | python
