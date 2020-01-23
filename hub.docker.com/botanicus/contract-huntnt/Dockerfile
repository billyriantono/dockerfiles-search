FROM aruneko/texlive

MAINTAINER Kazuma Miebori <km.isetan@gmail.com>

RUN apt-get update && apt-get upgrade -y && \
    apt-get install -y ca-certificates && \
    apt-get install -y python3-pip python3-wheel python3-setuptools python3-yaml jq wget perl fonts-noto

# pandoc (and pandoc-citeproc)
RUN wget -qO- https://api.github.com/repos/jgm/pandoc/releases/latest | \
    jq '.assets[] | select(.name | endswith(".deb")).browser_download_url' | \
    xargs wget -qO pandoc.deb && \
    dpkg -i pandoc.deb && rm -f pandoc.deb

# pandoc-crossref
RUN wget -qO- https://api.github.com/repos/lierdakil/pandoc-crossref/releases/latest | \
    jq '.assets[] | select(.name | startswith("linux")).browser_download_url' | \
    xargs wget -qO- | \
    tar xvz --strip-components 1 -C /usr/local/bin/

RUN python3 -m pip install --upgrade pip setuptools && \
    pip3 install --upgrade pandocfilters Pygments pandoc-minted

RUN tlmgr update --self \
    &&\
    tlmgr update --list \
    &&\
    tlmgr update --all \
    &&\
    tlmgr install collection-latexrecommended ec lm lm-math zapfding upquote type1cm \
    &&\
    tlmgr install luatexja pbibtex-base bxbase bxjscls zxjatype zxjafont \
    &&\
    tlmgr install collection-xetex collection-luatex adobemapping \
    &&\
    tlmgr install everyhook svn-prov mathpazo latexmk \
    &&\
    tlmgr install unicode-math noto babel-japanese zxjafbfont \
        xetex-pstricks pspicture biblatex biblatex-enc dvipng enumitem \
        pxjahyper cjk ipaex-type1 cjkutils collection-langcjk \
        bxcjkjatype texlive-ja logreq biber biblatex-iso690 \
        && \
    tlmgr path add
    
RUN apt purge -y wget jq \
    &&\
    apt autoremove -y \
    &&\
    apt clean \
    &&\
    rm -rf /var/lib/apt/lists

ENV LC_ALL ja_JP.UTF-8

CMD ["pandoc", "--help"]

VOLUME ["/workspace", "/root/.pandoc/templates"]
WORKDIR /workspace
