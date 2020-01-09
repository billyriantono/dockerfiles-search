FROM alpine:3.7

ENV PATH="/usr/local/texlive/2018/bin/x86_64-linuxmusl/:${PATH}"

RUN apk --no-cache add perl wget xz tar && \
    wget http://mirror.ctan.org/systems/texlive/tlnet/install-tl-unx.tar.gz && \
    mkdir /install-tl-unx && \
    tar -xvf install-tl-unx.tar.gz -C /install-tl-unx --strip-components=1 && \
    echo "selected_scheme scheme-basic" >> /install-tl-unx/texlive.profile && \
    /install-tl-unx/install-tl -profile /install-tl-unx/texlive.profile && \
    tlmgr install babel-french && \
    tlmgr install collection-fontsrecommended && \
    tlmgr install pdfpages && \
    apk del perl wget xz tar && \
    rm -r /usr/local/texlive/2018/texmf-dist/doc && \
    rm -r /usr/local/texlive/2018/texmf-dist/source && \
    rm -r /usr/local/texlive/2018/texmf-dist/fonts/afm/adobe && \
    rm -r /usr/local/texlive/2018/texmf-dist/fonts/afm/bitstrea && \
    rm -r /usr/local/texlive/2018/texmf-dist/fonts/afm/hoekwater && \
    rm -r /usr/local/texlive/2018/texmf-dist/fonts/afm/urw && \
    rm -r /usr/local/texlive/2018/texmf-dist/fonts/afm/public/cm-super && \
    rm -r /usr/local/texlive/2018/texmf-dist/fonts/afm/public/lm && \
    rm -r /usr/local/texlive/2018/texmf-dist/fonts/afm/public/tex-gyre && \
    rm -r /usr/local/texlive/2018/texmf-dist/fonts/tfm/adobe && \
    rm -r /usr/local/texlive/2018/texmf-dist/fonts/tfm/bitstrea && \
    rm -r /usr/local/texlive/2018/texmf-dist/fonts/tfm/monotype && \
    rm -r /usr/local/texlive/2018/texmf-dist/fonts/tfm/urw35vf && \
    rm -r /usr/local/texlive/2018/texmf-dist/fonts/tfm/public/tex-gyre && \
    rm -r /usr/local/texlive/2018/texmf-dist/fonts/type1/adobe && \
    rm -r /usr/local/texlive/2018/texmf-dist/fonts/type1/bitstrea && \
    rm -r /usr/local/texlive/2018/texmf-dist/fonts/type1/hoekwater && \
    rm -r /usr/local/texlive/2018/texmf-dist/fonts/type1/urw && \
    rm -r /usr/local/texlive/2018/texmf-dist/fonts/type1/public/cm-super && \
    rm -r /usr/local/texlive/2018/texmf-dist/fonts/type1/public/tex-gyre && \
    rm -r /usr/local/texlive/2018/texmf-dist/fonts/type1/public/tipa && \
    rm -r /install-tl-unx && \
    rm install-tl-unx.tar.gz

CMD ["/bin/sh"]
