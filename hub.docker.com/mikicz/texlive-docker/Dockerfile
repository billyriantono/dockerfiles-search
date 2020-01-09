FROM fedora:30

RUN dnf install -y java-1.8.0-openjdk

# we need the command pygmentize - but it doesn't get created when python-pygments is installed, ergo:
RUN pip3 install pygments

RUN dnf install -y texlive \
                   texlive-dirtree \
                   texlive-arara \
                   texlive-floatrow \
                   texlive-xltxtra \
                   texlive-polyglossia \
                   texlive-minted \
                   texlive-framed \
                   texlive-glossaries \
                   texlive-biblatex \
                   texlive-biblatex-iso690 \
                   texlive-blindtext \
                   texlive-standalone \
                   texlive-aeguill \
                   texlive-appendixnumberbeamer \
                   texlive-a4wide \
                   texlive-nag \
                   texlive-emptypage \
                   texlive-was \
                   texlive-multirow \
                   texlive-algorithmicx \
                   texlive-tcolorbox \
                   texlive-dashrule \
                   texlive-fontawesome \
                   texlive-tocloft \
                   biber \
                   dejavu-sans-mono-fonts \
                   linux-libertine-fonts \
                   linux-libertine-biolinum-fonts \
                   graphviz \
                   inkscape \
                   make \
                   findutils \
                   git \
                   google-crosextra-carlito-fonts \
                   wget \
                   which

