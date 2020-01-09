FROM opensuse/leap:15.0
MAINTAINER Pascal Hebbeker <pascal.hebbeker@natur.cuni.cz>

RUN zypper install -y make
RUN zypper install -y git
RUN zypper install -y \
      texlive-latex-bin-bin \
      texlive-latexpand \
      texlive-todonotes \
      texlive-latexmk \
      texlive-extsizes \
      texlive-sectsty \
      texlive-lastpage \
      texlive-droid \
      texlive-titlesec \
      texlive-natbib \
      texlive-preprint \
      texlive-psnfss \
      texlive-caption \
      texlive-float \
      texlive-babel-english \
      texlive-fancyhdr \
      texlive-siunitx \
      texlive-setspace \
      texlive-csquotes \
      texlive-charter \
      texlive-helvetic \
      texlive-courier \
      texlive-txfonts \
      texlive-dvips \
      texlive-bibtex-bin \
      texlive-enumitem \
      texlive-chktex-bin \
      texlive-ulem \
      texlive-times \
      texlive-epstopdf-bin \
      texlive-pdfjam-bin \
      texlive-revtex4 \
      texlive-revtex \
      texlive-mhchem \
      texlive-acro
RUN zypper install -y zip unzip
RUN zypper install -y texlive-pythontex texlive-pythontex-bin
RUN zypper install -y texlive-latexdiff-bin
RUN perl -MCPAN -e 'install Algorithm::Diff'
RUN mkdir cwd
RUN zypper clean --all
