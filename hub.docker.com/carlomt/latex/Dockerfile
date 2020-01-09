FROM ubuntu:18.04
RUN apt-get -y update && apt-get -y upgrade
RUN DEBIAN_FRONTEND=noninteractive apt-get -y \
install luatex \
# texlive-base \
texlive-full \
texlive-luatex \
pandoc \
latexmk \
texlive \
texlive-xetex \
tex4ht \
texlive-latex-extra \
texlive-fonts-extra \
texlive-lang-italian \
texlive-science \
texlive-bibtex-extra \
html-xml-utils \
git \
make \
sudo \
tidy \
cmake

RUN git clone https://github.com/michal-h21/make4ht.git make4ht
RUN cd make4ht && make && make install

RUN git clone https://github.com/michal-h21/tex4ebook.git tex4ebook
RUN cd tex4ebook && make && make install
