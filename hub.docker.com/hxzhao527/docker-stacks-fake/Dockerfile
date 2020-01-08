FROM hxzhao527/docker-stacks-fake:base

LABEL maintainer="hxzhao <haoxiangzhao@outlook.com>"

ADD _inside/texlive.profile /tmp/notebook/texlive.profile

RUN apk add --no-cache git vim curl wget unzip xz fontconfig perl &&\
    cd /tmp/notebook &&\
    wget https://github.com/jgm/pandoc/releases/download/2.2.1/pandoc-2.2.1-linux.tar.gz &&\
    tar xzf pandoc-2.2.1-linux.tar.gz &&\
    cp pandoc-2.2.1/bin/pandoc* /usr/bin/ &&\
    cd /tmp/notebook &&\
    wget http://mirror.ctan.org/systems/texlive/tlnet/install-tl-unx.tar.gz &&\
    tar xzf install-tl-unx.tar.gz &&\
    install-tl-20*/install-tl --profile /tmp/notebook/texlive.profile --repository http://mirrors.ustc.edu.cn/CTAN/systems/texlive/tlnet/ &&\
    export PATH=$PATH:/usr/local/texlive/2018/bin/x86_64-linuxmusl/ &&\
    tlmgr install adjustbox collectbox ucs enumitem collection-fontsrecommended &&\
    cd / &&\
    rm -r /tmp/notebook
ENV PATH="$PATH:/usr/local/texlive/2018/bin/x86_64-linuxmusl/"
