FROM haskell:8.0

# Forked from https://github.com/jagregory/pandoc-docker
MAINTAINER James Gregory <james@jagregory.com>
MAINTAINER Donovan Fournier <support@dfournier.me>

# will ease up the update process
# updating this env variable will trigger the automatic build of the Docker image
ENV PANDOC_VERSION "2.1.1"

# install latex packages and utility packages
RUN apt-get update -y \
  && apt-get install -y --no-install-recommends \
    texlive-latex-base \
    texlive-xetex latex-xcolor \
    texlive-math-extra \
    texlive-latex-extra \
    texlive-fonts-extra \
    texlive-bibtex-extra \
    fontconfig \
    lmodern \
		ca-certificates \
		curl \
		wget \
    unzip \
	&& rm -rf /var/lib/apt/lists/*

# install pandoc
RUN cabal update && cabal install pandoc-${PANDOC_VERSION}

WORKDIR /source

CMD ["--help"]
