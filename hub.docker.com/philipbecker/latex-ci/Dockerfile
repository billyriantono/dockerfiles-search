FROM debian:jessie

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

ARG WGET=wget
ARG GIT=git
ARG MAKE=make
ARG PANDOC=pandoc
ARG PYGMENTS=python-pygments

RUN apt-get update && apt-get install -y \
  texlive-full \
  biber \
  "$WGET" \
  "$GIT" \
  "$MAKE" \
  "$PANDOC" \
  "$PYGMENTS" && \
  apt-get --purge remove -y .\*-doc$ && \
  apt-get clean -y
