FROM joni/ubuntu-box

RUN sudo apt-get update        && \
    sudo apt-get install -yq      \
             texlive-full         \
             texlive-xetex        \
             inkscape             \
             qpdf                 \
             exiftool             \
             biber             && \
    sudo apt-get clean         && \
    sudo rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

RUN wget -O - http://mirrors.ctan.org/macros/latex/contrib/titlesec.zip > \
        /tmp/titlesec.zip                                          && \
    unzip /tmp/titlesec.zip                                        && \
    sudo rm -rf /usr/share/texlive/texmf-dist/tex/latex/titlesec   && \
    sudo mv titlesec /usr/share/texlive/texmf-dist/tex/latex/      && \
    rm /tmp/titlesec.zip
