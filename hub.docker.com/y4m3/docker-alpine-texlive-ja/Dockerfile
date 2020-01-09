FROM frolvlad/alpine-glibc

MAINTAINER y4m3

ENV PATH /usr/local/texlive/2018/bin/x86_64-linuxmusl:$PATH

RUN apk update && \
    apk --no-cache add \
        fontconfig-dev \
        perl \
        tar \
        wget \
        xz

RUN mkdir /tmp/install-tl-unx && \
    wget -qO - ftp://tug.org/historic/systems/texlive/2018/install-tl-unx.tar.gz | \
    tar -xz -C /tmp/install-tl-unx --strip-components=1 && \
    printf "%s\n" \
        "selected_scheme scheme-basic" \
        "option_doc 0" \
        "option_src 0" \
        > /tmp/install-tl-unx/texlive.profile && \
    /tmp/install-tl-unx/install-tl \
        --profile=/tmp/install-tl-unx/texlive.profile && \
    tlmgr install \
        collection-basic \
        collection-latex \
        collection-latexrecommended \
        collection-latexextra \
        collection-fontsrecommended \
        collection-langjapanese \
        latexmk && \
    ( tlmgr install xetex || exit 0 ) && \
    rm -fr /tmp/install-tl-unx

RUN wget -q https://noto-website.storage.googleapis.com/pkgs/NotoSansCJKjp-hinted.zip && \
    wget -q https://noto-website.storage.googleapis.com/pkgs/NotoSerifCJKjp-hinted.zip && \
    mkdir -p /usr/local/texlive/texmf-local/fonts/opentype/google/notosanscjk/ && \
    mkdir -p /usr/local/texlive/texmf-local/fonts/opentype/google/notoserifcjk/ && \
    unzip NotoSansCJKjp-hinted.zip -d /usr/local/texlive/texmf-local/fonts/opentype/google/notosanscjk/ && \
    unzip NotoSerifCJKjp-hinted.zip -d /usr/local/texlive/texmf-local/fonts/opentype/google/notoserifcjk/ && \
    rm NotoSansCJKjp-hinted.zip && \
    rm NotoSerifCJKjp-hinted.zip && \
    mktexlsr

RUN apk --no-cache del xz tar fontconfig-dev

RUN apk --no-cache add bash

RUN mkdir /workdir

WORKDIR /workdir

VOLUME ["/workdir"]

CMD ["/bin/bash"]
