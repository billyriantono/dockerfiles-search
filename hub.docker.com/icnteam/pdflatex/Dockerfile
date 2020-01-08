FROM ubuntu:18.04
LABEL maintainer="Luca Muscariello <luca.muscariello@gmail.com>"

RUN apt-get update && apt-get install -y --no-install-recommends \
    texlive texlive-latex-recommended \
    texlive-latex-extra \
 && rm -rf /var/lib/apt/lists/* \
 && apt-get autoremove -y && apt-get clean -y
