FROM haskell:8.0

ADD entrypoint.sh /docker-entrypoint.sh
ENV PANDOC_VERSION "2.1.3"

RUN apt-get update -y \
  && apt-get install -y -o Acquire::Retries=10 --no-install-recommends \
    texlive-latex-base \
    texlive-xetex latex-xcolor \
    texlive-math-extra \
    texlive-latex-extra \
    texlive-fonts-extra \
    texlive-bibtex-extra \
    fontconfig \
    lmodern \
  && rm -rf /var/lib/apt/lists/* \
  && chmod +x /docker-entrypoint.sh \
  && cabal update && cabal install pandoc-${PANDOC_VERSION}

WORKDIR /source

ENTRYPOINT ["/docker-entrypoint.sh"]

CMD ["--help"]
