FROM alpine:3.9

COPY texlive-profile.txt /tmp/

# set up packages
RUN apk add --no-cache wget perl xz git gnuplot ghostscript biber make python3 && \
    wget http://mirror.ctan.org/systems/texlive/tlnet/install-tl-unx.tar.gz && \
    tar -xzf install-tl-unx.tar.gz && \
    install-tl-20*/install-tl --profile=/tmp/texlive-profile.txt && \
    rm -rf install-tl-* && \
    rm -rf /var/lib/apt/lists/*

ENV PATH=/usr/local/texlive/bin/x86_64-linuxmusl:$PATH

RUN tlmgr update --self && \
tlmgr install \
latex latex-bin latexmk collection-fontsrecommended standalone xkeyval tikz-cd pgf pgfplots graphics xcolor tools epstopdf luatex85 pdfcrop tikz-qtree preview \
geometry koma-script oberdiek babel-english babel-german csquotes etoolbox amsmath amscls algorithms algorithmicx float preprint caption cleveref xstring footmisc biblatex biber biblatex-ieee logreq url booktabs \
beamer ec lm tcolorbox environ trimspaces wasysym changes xifthen ifmtarg ulem todonotes truncate xpatch l3kernel l3backend l3packages wasy hyperref stmaryrd mathtools was translator a0poster svg pstricks breqn xint iftex pst-grad pst-blur multirow colortbl gnuplottex moreverb framed filecontents times adjustbox collectbox a4wide ntgclass fancyhdr pst-tools psnfss listings
