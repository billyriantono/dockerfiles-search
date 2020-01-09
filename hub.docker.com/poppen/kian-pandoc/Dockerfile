FROM poppen/alpine-pandoc-ja:2.7.3-texlive2019

ARG KIAN_VERSION=06

ADD kian-v${KIAN_VERSION}.zip /tmp

WORKDIR /usr/local/texlive/texmf-local/tex/latex
RUN apk --no-cache add --virtual .build-deps \
    unzip \
 && unzip /tmp/kian-v${KIAN_VERSION}.zip "kian/*"

WORKDIR /usr/local/texlive/texmf-local/tex/latex/kian
RUN mktexlsr \
 && rm -rf /tmp/* \
 && apk del .build-deps

WORKDIR /workspace
