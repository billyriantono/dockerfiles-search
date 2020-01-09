FROM haskell:8.4
MAINTAINER Jan Philip Bernius <janphilip@bernius.net>

# Set to Non-Interactive
ENV DEBIAN_FRONTEND noninteractive

# Install all TeX and LaTeX dependences
RUN apt-get update && \
  apt-get install --yes --no-install-recommends \
  make \
  git \
  ca-certificates \
  locales \
  lmodern \
  texlive-latex-base \
  texlive-fonts-recommended \
  texlive-fonts-extra \
  texlive-generic-recommended \
  texlive-lang-japanese \
  latex-xcolor \
  texlive-math-extra \
  texlive-latex-extra \
  texlive-extra-utils \
  texlive-bibtex-extra \
  biber \
  fontconfig \
  # texlive-xetex && \
  texlive-luatex && \
  apt-get autoclean && apt-get --purge --yes autoremove && \
  rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

# Install Pandoc
RUN cabal update && cabal install \
  pandoc \
  pandoc-citeproc \
  pandoc-citeproc-preamble \
  pandoc-crossref

# Set the locale
# RUN update-locale LANG=ja_JP.UTF-8 LANGUAGE="ja_JP:ja"
RUN dpkg-reconfigure locales

# Export the output data
WORKDIR /data
VOLUME ["/data"]

ENTRYPOINT ["pandoc"]

CMD ["--help"]
