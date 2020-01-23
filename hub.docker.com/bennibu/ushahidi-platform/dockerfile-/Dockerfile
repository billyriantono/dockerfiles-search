FROM ubuntu:latest

RUN apt-get update && apt-get install -y \
    build-essential \
    pandoc \
    python-pip \
    texlive \
    texlive-generic-extra \
    texlive-latex-recommended \
    texlive-latex-extra \
    texlive-fonts-recommended \
 && rm -rf /var/lib/apt/lists/*

RUN pip install -U pip && pip install \
    Sphinx \
    sphinx_rtd_theme

WORKDIR /docs
VOLUME /docs

CMD ["/bin/bash"]
