
FROM haskell:8.6

LABEL maintainer="julien.rollin@gmail.com"

ENV PANDOC_VERSION "2.7.3"

# install latex and recommanded packages
RUN apt-get update -y \
        && apt-get install -y --no-install-recommends \
        texlive-latex-base \
        texlive-fonts-recommended \
        texlive-xetex latex-xcolor \
        texlive-math-extra \
        texlive-latex-extra \
        texlive-fonts-extra \
        texlive-bibtex-extra \
        fontconfig \
        lmodern


# install pandoc
RUN cabal new-update && cabal new-install pandoc-${PANDOC_VERSION}

WORKDIR /source

ENTRYPOINT ["/root/.cabal/bin/pandoc"]

CMD ["--version"]