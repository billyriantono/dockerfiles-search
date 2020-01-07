FROM debian:buster-slim

LABEL maintainer="Kimiaki Kuno <knokmki612@gmail.com>"

RUN apt-get update \
 && apt-get install -y texlive-lang-japanese texlive-latex-extra latexmk biber \
 && rm -rf /var/lib/apt/lists/*
RUN kanji-config-updmap-sys ipaex

WORKDIR /workdir

VOLUME ["/workdir"]

CMD ["bash"]
