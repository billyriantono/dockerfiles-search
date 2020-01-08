FROM ubuntu:latest

RUN apt-get update && apt-get install --no-install-recommends -y \
        curl \
        ca-certificates \
        latexmk \
        make \
        biber \
        cm-super \
        lmodern \
        texlive-base \
        texlive-bibtex-extra \
        texlive-binaries \
        texlive-fonts-extra \
        texlive-fonts-extra-links \
        texlive-fonts-recommended \
        texlive-latex-base \
        texlive-latex-extra \
        texlive-latex-recommended \
        texlive-metapost \
        texlive-pictures \
        texlive-plain-generic \
        texlive-pstricks \
        texlive-publishers \
        texlive-science \
        texlive-xetex \
&& rm -rf /var/lib/apt/lists/*