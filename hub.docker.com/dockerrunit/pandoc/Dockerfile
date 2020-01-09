FROM haskell:8.0

RUN apt-get update && apt-get install -y --no-install-recommends \
        lmodern \
        texlive-lang-cjk \
        texlive-luatex \
        texlive-math-extra \
        texlive-xetex \
        && apt-get clean \
        && rm -rf /var/lib/apt/lists/*

RUN cabal update && cabal install \
        pandoc \
        pandoc-crossref \
        pandoc-citeproc \
        && rm -rf ~/.cabal/packages ~/.cabal/logs

ENV PANDOCPATH /pandoc
WORKDIR $PANDOCPATH

ENTRYPOINT ["pandoc"]
