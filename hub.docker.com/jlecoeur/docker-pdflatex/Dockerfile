FROM ubuntu:xenial

MAINTAINER Julien Lecoeur <julien.lecoeur@gmail.com>

RUN apt-get update \
    && DEBIAN_FRONTEND=noninteractive apt-get -y --quiet --no-install-recommends install \
        texlive-latex-recommended \
        texlive-latex-extra \
        texlive-fonts-recommended \
        texlive-fonts-extra \
        texlive-lang-all \
        texlive-font-utils \
        texlive-extra-utils \
        ghostscript \
        git \
        ssh \
        make

CMD ["/bin/bash"]
