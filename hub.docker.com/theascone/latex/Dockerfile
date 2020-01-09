FROM debian:jessie

RUN apt-get update && apt-get install -y texlive-full biber latexmk make
RUN useradd -m latex
WORKDIR /home/latex
USER latex
