FROM debian:9
LABEL authors="Sebastien Chassot (sinux)"

# Set the env variables to non-interactive
ENV DEBIAN_FRONTEND noninteractive
ENV DEBIAN_PRIORITY critical
ENV DEBCONF_NOWARNINGS yes

RUN apt-get update -y \
  && apt-get install -y --no-install-recommends \
    fontconfig \
    make \
    pandoc \
    texlive-bibtex-extra \
    texlive-fonts-extra \
    texlive-fonts-recommended \
    texlive-latex-base \
    texlive-latex-extra \
    texlive-math-extra \
    texlive-xetex latex-xcolor \
    transfig \
    librsvg2-2 \
    wget \
	vim net-tools librsvg2-bin lmodern texlive-lang-french \
  && rm -rf /var/lib/apt/lists/*

RUN wget --no-check-certificate https://github.com/jgm/pandoc/releases/download/2.6/pandoc-2.6-1-amd64.deb && \
    dpkg -i pandoc* && \
    rm pandoc* && \
    apt-get clean

RUN mkdir -p /build/pdf
COPY Makefile /build/
COPY README.md /build/
COPY template/* /build/pdf/

WORKDIR /build

CMD ["cat", "README.md"]
