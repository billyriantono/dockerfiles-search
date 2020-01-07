FROM debian:stable

ARG USER_NAME=latex
ARG USER_HOME=/home/latex
ARG USER_ID=1000
ARG USER_GECOS=LaTeX

RUN adduser \
  --home "$USER_HOME" \
  --uid $USER_ID \
  --gecos "$USER_GECOS" \
  --disabled-password \
  "$USER_NAME"

RUN apt-get update && apt-get install -y \
  texlive-full \
  aspell-en \
  wget \
  git \
  make \
  pandoc \
  latexmk && \
  apt-get --purge remove -y .\*-doc$ && \
  apt-get clean -y

WORKDIR /app
