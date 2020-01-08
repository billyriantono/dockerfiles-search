
FROM cmch/emacs:locale

ARG DEBIAN_FRONTEND=noninteractive

RUN \
    sed \
    -e 's/# \(en_US.UTF-8 UTF-8\)/\1/' \
    -e 's/# \(zh_TW\)/\1/' \
    /etc/locale.gen -i \
    && locale-gen
