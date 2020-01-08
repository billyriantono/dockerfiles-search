FROM ruby:2.5

# setup latex user
ARG USERNAME=latex
ARG USERHOME=/home/latex
ARG USERID=1000
ARG USERGECOS=LaTEX

RUN adduser \
  --home "$USERHOME" \
  --uid $USERID \
  --gecos "$USERGECOS" \
  --disabled-password \
  "$USERNAME"

# install args
ARG WGET=wget
ARG GIT=git
ARG MAKE=make
ARG PANDOC=pandoc
ARG PYGMENTS=python-pygments
ARG XZDEC=xzdec
ARG GHOSTS=ghostscript

# copy texlive install profile to tmp
COPY texlive-full.profile /tmp/

# main install
RUN apt-get update \
  && apt-get install -y \
  # some auxiliary tools
  "$WGET" \
  "$GIT" \
  "$MAKE" \
  # markup format conversion tool
  "$PANDOC" \
  # Required for syntax highlighting using minted.
  "$PYGMENTS" \
  # Required for tlmgr under debian
  "$XZDEC" \
  # Required for ImageMagick to convert PDF to Image
  "$GHOSTS" \
  # install latest texlive
  && wget "http://mirror.ctan.org/systems/texlive/tlnet/install-tl-unx.tar.gz" \
  && tar -xzf install-tl-unx.tar.gz \
  && cd install-tl-* \
  && ./install-tl -no-gui -profile /tmp/texlive-full.profile \
  && cd ../ \
  # cleanup install
  && rm -rf install-tl-* /tmp/texlive-full.profile

# path recommendation: https://github.com/bundler/bundler/pull/6469#issuecomment-383235438
ENV PATH /opt/texlive/bin/x86_64-linux:$PATH

# init user tree for tlmgr
RUN tlmgr --usermode init-usertree \
  # Remove unnecessary stuff
  && apt-get clean -y
