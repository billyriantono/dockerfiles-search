FROM debian:stable

ENV DEBIAN_FRONTEND noninteractive

LABEL maintainer="janic.mikes@gmail.com"

RUN apt-get update && \
    apt-get install -y \
        texlive-xetex \
        texlive-lang-german \
        texlive-bibtex-extra \
        biber \
        latexmk

WORKDIR /doc

ENTRYPOINT ["latexmk"]
CMD ["-help"]