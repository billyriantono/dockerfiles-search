FROM fedora:29
RUN dnf -y install latexmk texlive-collection-fontsrecommended texlive-import texlive-babel-english texlive-glossaries texlive-textcase texlive-multirow texlive-xstring texlive-menukeys texlive-fancyhdr
RUN dnf -y install git
RUN dnf -y install make
RUN mkdir /vsc_user_docs
WORKDIR /vsc_user_docs
CMD make all
