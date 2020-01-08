FROM ubuntu:16.10

RUN apt-get update && \
    apt-get install -y python python-pip texlive-latex-recommended texlive-latex-extra texlive-fonts-recommended && \
    pip install Sphinx sphinx_rtd_theme sphinxcontrib-blockdiag sphinxcontrib-actdiag sphinxcontrib-nwdiag sphinxcontrib-seqdiag sphinxcontrib-napoleon sphinxcontrib-httpdomain && \
    rm -rf /var/lib/apt/lists/*

WORKDIR /sphinx
