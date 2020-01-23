# FROM cmch/python:10-slim
# FROM cmch/python:locales
FROM cmch/python:emacs

ARG DEBIAN_FRONTEND=noninteractive

RUN \
    apt update && apt install -yq  \
    locales \
    && sed \
    -e 's/# \(en_US.UTF-8 UTF-8\)/\1/' \
    -e 's/# \(zh_TW\)/\1/' \
    /etc/locale.gen -i \
    && locale-gen
